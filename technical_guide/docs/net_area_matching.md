# Introduction

This documentation, intended for developers, aims to present details on how the process of harmonizing area features at borders works, as well as the technical principles and configuration of the tool.

# Installation

## Source Code 

The application's source code is available in the [net_area_matching](https://github.com/openmapsforeurope2/net_area_matching.git) repository.

## Dependencies 

Installing the application requires compiling internal and external libraries, including those from IGN.

Here is the dependency graph:

<img src="images/dependencies.png" width="500" height="auto">

### IGN Socle 

IGN's software core brings together a set of internally developed libraries that unify access to C++ libraries for processing and storing geographic data.  
It provides, among other things, pivot data models (geometries, attribute objects), reading/writing functions for object containers, geometry operations, many algorithms, etc.

The source code for the socle is available in the [sd-socle](http://gitlab.forge-idi.ign.fr/socle/sd-socle.git) repository.

### LibEPG 

This library, developed at IGN and mainly relying on the software socle, contains many algorithms and utility functions specifically dedicated to OME2 production needs.  
It essentially includes generalization functions, utilities for process management such as logging, orchestration, context management).  
It also provides operators for encapsulating complex geometric objects to optimize their manipulation (using graphs, indexes, etc.), thus improving processing performance.

The source code for the libepg library is available at [libepg](http://gitlab.dockerforge.ign.fr/europe/libepg.git).

# Configuration

The tool relies on many configuration parameters to adapt algorithm behavior based on national specificities (semantics, precision, scale, conventions, etc.).

In the [configuration folder](https://github.com/openmapsforeurope2/net_area_matching/tree/main/config), you will find the following files:

- epg_parameters.ini: gathers basic parameters from the libepg library, which forms the development core of the tool. This file also acts as a master file, pointing to additional configuration files.
- db_conf.ini: database connection information.
- theme_parameters.ini: configuration of parameters specific to the application.

# Process Functionality

The harmonization process for area features is launched for a pair of neighboring countries.

## Preliminary Steps

The data on which this process is launched must first be cleaned using the **clean** tool from the [data-tools](https://github.com/openmapsforeurope2/data-tools) project, which removes features outside the country or that are too far from the border.  
This tool should be used on working tables containing extracted data from both countries in the region around their common border.

## General Principle of the Process

The area feature harmonization process is broken down into a series of key steps.
To orchestrate the sequence of these steps, the application uses the **epg::step::StepSuite** tool from the **libepg** library. This allows running a succession of **epg::step::Step** operations, each representing a transformation or process step.
Each step is assigned a code (a three-digit number). Steps are numbered in order. If a step transforms the data it works on, a new table is created for the result, named with the step code as a prefix.  
This ensures that intermediate results are kept, allowing the process to be interrupted and resumed, and facilitating debugging.

The main steps are as follows:

**301** - import 'standing water' objects into the working table  
**310** - generation of 'cutting lines'  
**320** - removal of areas outside their country  
**330** - cleanup of orphan 'cutting lines'  
**334** - creation of intersection areas between both countries, stored in a dedicated table  
**335** - generation of 'cutting points'  
**340** - merging of overlapping areas between both countries  
**350** - splitting of merged areas using 'cutting lines' and sections from 'cutting points'  
**360** - assignment of attributes to the merged/split areas  
**370** - aggregation of merged/split areas  
**399** - export of 'standing water' areas

The **epg::step::StepSuite** tool allows running only selected steps or a range of steps.

## Running the Process

Example: run the complete process for France (country code 'fr') and Belgium (country code 'be'):
```
net_area_matching --c path/to/config/epg_parameters.ini --cc be#fr
```
Note: the `--cc` parameter specifies the code for the border between the two countries. The country code is always composed by concatenating the two country codes separated by a '#'.

Example: run a single step:
```
net_area_matching --c path/to/config/epg_parameters.ini --cc be#fr --sp 340
```

Example: run a range of steps:
```
net_area_matching --c path/to/config/epg_parameters.ini --cc be#fr --sp 340-370
```
Here, all steps from 340 to 370 (inclusive) will be executed.

## Step-by-Step Details

### 301: AddStandingWater

'Standing water' objects from both countries' working tables are copied into the 'watercourse areas' working table. The copied objects are removed from the 'standing water' table.

![301_with_key](images/301_with_key.png)

#### Working Data:

| table                          | input | output | working entity | description                                                 |
|--------------------------------|-------|--------|----------------|-------------------------------------------------------------|
| AREA_TABLE_INIT                | X     | X      | X              | areas to process                                            |
| AREA_TABLE_INIT_STANDING_WATER | X     | X      | X              | areas to export into AREA_TABLE_INIT                        |

#### Main Calculation Operators Used:
- app::calcul::StandingWaterOp

#### Processing Description:
Parameters used:
| parameter              | description                                                          |
|------------------------|----------------------------------------------------------------------|
| IS_STANDING_WATER_NAME | name of the field indicating if the object is 'standing water'       |

A _IS_STANDING_WATER_NAME_ column of type _character varying(255)_ is added to _AREA_TABLE_INIT_ and filled for each imported object.  
The process removes imported objects from _AREA_TABLE_INIT_STANDING_WATER_.

### 310: GenerateCuttingLines

Objective: generate _'cutting lines'_, i.e., portions of contours shared by two polygons of the same country.

#### Working Data:

| table           | input | output | working entity | description                  |
|-----------------|-------|--------|----------------|------------------------------|
| AREA_TABLE_INIT | X     | X      | X              | areas to process             |
| CUTL_TABLE      |       | X      |                | table of 'cutting lines'     |

Note: the _CUTL_TABLE_ output is not prefixed with the step number (it serves as a reference for the whole process).

CUTL_TABLE is dropped and recreated if it exists. Structure:

| field             | type                   |
|-------------------|------------------------|
| COUNTRY_CODE      | character varying(8)   |
| LINKED_FEATURE_ID | character varying(255) |
| GEOM              | LineStringZ            |

#### Main Calculation Operators Used:
- app::calcul::StandingWaterOp

#### Processing Description:
Processing is done country by country. The principle is to build a planar graph from all polygon contours of a country, then identify arcs shared by two surfaces.

![310_with_key](images/310_with_key.png)

### 320: CleanByLandmask

Objective: remove areas and area parts too far from their country.

#### Working Data:

| table                 | input | output | working entity | description                   |
|-----------------------|-------|--------|----------------|-------------------------------|
| AREA_TABLE_INIT       | X     | X      | X              | areas to process              |
| TARGET_BOUNDARY_TABLE | X     |        |                | borders                       |
| LANDMASK_TABLE        | X     |        |                | national landmasks            |

#### Main Calculation Operators Used:
- app::calcul::PolygonSplitterOp
- app::calcul::PolygonCleanerOp
- app::calcul::PolygonMergerOp

#### Processing Description:
##### 1) Area Splitting

Parameters used:
| parameter              | description                                           |
|------------------------|-------------------------------------------------------|
| LAND_COVER_TYPE_NAME   | name of the land cover type field                     |
| LAND_COVER_TYPE_VALUE  | value for the land cover type                         |
| PS_BORDER_OFFSET       | offset distance for cutting geometry from the border  |

Areas extending beyond their country are cut along lines corresponding to the international borders, offset by a certain distance outside the country.

![320_with_key](images/320_with_key.png)

To optimize calculations, the cutting geometry contouring the country is indexed in the quadtree of the **epg::tools::geometry::SegmentIndexedGeometryCollection** class.

##### 2) Removal of Areas Outside the Country

Parameters used:
| parameter              | description                                           |
|------------------------|-------------------------------------------------------|
| LAND_COVER_TYPE_NAME   | name of the land cover type field                     |
| LAND_COVER_TYPE_VALUE  | value for the land cover type                         |
| PC_DISTANCE_THRESHOLD  | minimum distance threshold for removing areas         |

Areas outside their country and further than a certain threshold are removed.

![320_2_with_key](images/320_2_with_key.png)

For optimization, a working area corresponding to the border zone of the country is precomputed as the intersection of a buffer and the national landmask.

_Note: the buffer radius (work zone depth) must be greater than or equal to the extraction distance (data-tools::border_extract parameter)._

##### 3) Merge of Cut Areas

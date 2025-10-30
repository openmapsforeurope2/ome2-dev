# Define international boundaries for OME2

For the OME2 project, in order to harmonise data across countries, it is necessary to use common international boundaries. However, neighbouring countries often provide different geometries for their international boundaries, even when these are officially agreed.

An FME workbench was therefore put into place to calculate common “technical” boundaries, which are considered as a reference for the project: boundary_unification_process

## 1. How to use the workbench
This workbench is divided into 8 steps. Each step produces output tables which are then used as input in the following step.
The steps have to be launched one by one, in order to allow for some manual work in between.
Before launching a step, make sure to:
- Activate the tables which need to be read.
- Deactivate any link from these tables to transformers from other steps (cf. steps 2.1 and 4.1).

## 2. Workbench description
Example: BE#NL
Pre-requisite: both countries’ administrative units themes need to have been included in the OME2 database. There must be a country polygon for each country in the au.administrative_unit_area_1 table (or possibly several polygons in case of islands etc.).
The au.administrative_unit_area_1 from the OME2 PostgreSQL database will be used as source data for the process.

### Step 0 (FME): Configure workbench
The workbench parameters first need to be configured directly in the workbench:

 <img width="388" height="243" alt="image" src="https://github.com/user-attachments/assets/8cece253-f3d9-4abe-b968-6d0d59865061" />
 
There are three of them:
- Country code 1: country code of the first country to be processed in alphabetical order (referred to as “cc1” in the document).
- Country code 2: country code of the second country to be processed in alphabetical order (referred to as “cc2” in the document).
- OME2 database: name of the database connection configured in FME which gives access to the PostgreSQL OME2 database. If the connection does not exist in FME, it needs to be created first.

### Step 1.1 (FME): Extract outer international boundaries from administrative units.
#### Input:
- au.administrative_unit_area_1
#### TO-DO in FME:
- Enable only the au.administrative_unit_area_1 feature type (Step 1.1 frame).
- Run workbench.
#### Steps description:
1.	For each country, dissolve administrative units into single part polygons.
2.	Extract edges from the dissolved polygons  these are the outer boundaries, which then need to be cleaned.
3.	Slightly simplify these outer boundaries to avoid having too many vertices (Douglas-Peucker algorithm with a 10-cm tolerance).
4.	Gather edges from the two countries into a single table and planarize the data.
5.	Merge the lines to remove pseudo-nodes: the remaining lines are split only where at least 3 objects intersect.

<img width="945" height="192" alt="image" src="https://github.com/user-attachments/assets/72fe3e53-90f8-4e4b-827a-b39cc097e3fd" />

#### Output:
- public._intbnd1_ lines (backup copy)
- public._intbnd1_lines_corrected (to be corrected in the next step).

<img width="522" height="447" alt="image" src="https://github.com/user-attachments/assets/6794a103-e4e1-4823-a1af-96f460fad235" />

Since we are working on the BE#NL international boundary, all lines which do not belong to this boundary need to be deleted manually in the next step.

## Step 1.2 (manual): Clean the outer edges to keep only BE#NL data 

#### Input:
- public._intbnd1_ lines_corrected (before correction)

#### Steps to be performed (in QGIS for example):
1.	Manually delete the lines which do not correspond to the BE#NL boundary (coastlines, boundaries with other countries, Belgian enclaves in Germany). To do that in QGIS you can:
- Activate snapping
- Use the “separate entities” tool to split lines where the boundary to be processed stops  
2.	If necessary, snap the endpoints of the two lines representing the BE and NL version of the main international boundary (for the test, it was necessary on the junction with Germany). If the neighbouring boundaries are already edge-matched, there should be an international_boundary_node object which should be used as reference (or updated if necessary). Otherwise, the endpoints should be snapped approximately in the middle of the space separating them (the distance is usually very small so the precise location is not very important).
3.	If there is no international_boundary_node object at the location of the new intersection, create one and fill its country_code attribute with the country codes of all intersecting countries, in alphabetical order and separated by a hash sign (#).








---------
> TO-DO: move to boundary_unification doc
> - When an isolated country is integrated, only the first step of the workbench needs to be used. This creates the boundary lines (including coastlines) all around the country.
> - Then the lines need to be split manually where there is a change in country code or boundary type (international boundary vs coastline).
> - Create point in ib.international_boundary_node when there is a change in the boundary line (type or country code).
> - Use EBM as reference.

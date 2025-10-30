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











> TO-DO: move to boundary_unification doc
> - When an isolated country is integrated, only the first step of the workbench needs to be used. This creates the boundary lines (including coastlines) all around the country.
> - Then the lines need to be split manually where there is a change in country code or boundary type (international boundary vs coastline).
> - Create point in ib.international_boundary_node when there is a change in the boundary line (type or country code).
> - Use EBM as reference.

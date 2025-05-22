# User guide for the production of the OME2 high-value large-scale dataset

## User guide to integrate a new country
When data is provided for a new country, here are the main steps to follow:
* Upload the data in a PostGIS database on the OME2 server.
* Convert the data to integrate it in the central database.
* Process international boundaries.
* If neighbouring countries are already included, edge-match the data for each theme successively, starting with Administrative units (AU).

These steps are detailed below.

### 1. Upload to PostGIS

### 2. Model conversion
National producers can either provide:
* national datasets in their own data model: in this case, they are required to provide a mapping table explaining how to transform their data into the OME2 data model.
* INSPIRE datasets: in this case, it is considered that the OME2 team is able to understand the transformation on their own, so no mapping table is required.

This data needs to be converted to the OME2 data model and integrated in the central database, using the [model conversion tool](https://github.com/openmapsforeurope2/data-model-transformer).
The model conversion tool needs one JSON configuration file per theme to run the transformation. Explanations on the implementation of the configuration files and on how to run the tool are available in its [documentation](https://github.com/openmapsforeurope2/data-model-transformer).


### 3. International boundaries


### 4. Edge-matching

#### 4.1. Administrative units theme (AU)
[User guide for AU matching](https://github.com/openmapsforeurope2/OME2/blob/main/docs/prod/administrative_unit_area_matching/user_guide_au.md)

#### 4.2. Transport network theme (TN)
* [Cleaning](https://github.com/openmapsforeurope2/OME2/blob/main/docs/prod/network_matching/steps/cleaning.md)
* [Network matching](https://github.com/openmapsforeurope2/OME2/blob/main/docs/prod/network_matching/steps/matching.md)
* [Integration](https://github.com/openmapsforeurope2/OME2/blob/main/docs/prod/network_matching/steps/integration.md)

#### 4.3. Hydrography theme (HY)
* [Cleaning](https://github.com/openmapsforeurope2/OME2/blob/main/docs/prod/network_matching/steps/cleaning.md)
* [Area matching]
* [Network matching](https://github.com/openmapsforeurope2/OME2/blob/main/docs/prod/network_matching/steps/matching.md)
* [Integration](https://github.com/openmapsforeurope2/OME2/blob/main/docs/prod/network_matching/steps/integration.md)

## User guide to update an existing country

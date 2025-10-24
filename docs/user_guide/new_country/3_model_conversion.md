# Model conversion

National producers can either provide:
* national datasets in their own data model: in this case, they are required to provide a mapping table explaining how to transform their data into the OME2 data model.
* INSPIRE datasets: in this case, it is considered that the OME2 team is able to understand the transformation on their own, so no mapping table is required.

This data needs to be converted to the OME2 data model and integrated in the central database, using the [model conversion tool](https://github.com/openmapsforeurope2/data-model-transformer).
The model conversion tool needs one JSON configuration file per theme to run the transformation. Explanations on the implementation of the configuration files and on how to run the tool are available in its [documentation](https://github.com/openmapsforeurope2/data-model-transformer).

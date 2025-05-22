
# Cleaning step

The "cleaning" step consists in deleting objects located outside of the country's extene and more than a certain distance away from its international boundaries. The default distance used is 5 meters.

This means that in OME2, we consider that objects provided by a country and located less than 5 meters away for the international boundary (even if they are in the neighbouring country's extent) can be kept. Objects located in the neighbouring country and more than 5 meters away from the international boundary are deleted by the cleaning step.

The cleaning step needs to be applied once new data has been integrated in the OME2 database and once the OME2 version of its international boundaries have been defined.

The cleaning step works like most steps in the OME2 process. At first, the data to be processed is stored in the "official" table (e.g. tn.road_link). The cleaning step is divided into 3 sub-steps:
* Sub-step 1: the relevant data is extracted in the corresponding working table (e.g. road_link_w). To do that, an extract distance needs to be defined (see below).
* Sub-step  2: the cleaning tool is applied to the working table (e.g. road_link_w) -> the objects located in the wrong country and more than 5 meters away from the boundary are deleted.
* Sub-step  3: the result is integrated in the original table (e.g. tn.road_link).

A single command line enables to perform the three sub-steps.

## Define the parameters
The cleaning tool needs two parameters: the extract distance and the cleaning distance.

#### Extract distance
The extract distance corresponds of the size of the buffer which will be created around the international boundary to extract the data for cleaning. It needs to be as small as possible in order to extract as little data as possible (so that the tool can run more efficiently) but large enough to contain all the objects located in the wrong country which need to be deleted.

To determine the extract distance, you can open the data in QGIS and approximately measure the distance between the international boundaries and the farthest objects. The extract distance parameter should be slightly higher than the distance measured in QGIS.

![Extract_distance_QGIS](https://github.com/openmapsforeurope2/OME2/blob/main/docs/images/Extract_distance_QGIS.png)

In the example above, the distance measured between the boundary and the farthest objects is ~17308 meters. To be safe, an extract distance of 20000 meters can be used.

#### Cleaning distance
The default value for the cleaning distance is 5 meters. This value was chosen empirically while testing the edge-matching process. 
There has been no reason to use a different value so far.


## Run the command line

/!\ TO BE UPDATED

```
python3 script/clean.py -c conf.json -d <distance> -T <theme> -t <net_type>_w <country_code>
```

The command lines and parameters used during the production of the HVLSP 2.0 and 3.0 can be found in the [clean_hy_tn.sh](https://github.com/openmapsforeurope2/data-tools/blob/main/use_case/clean_hy_tn.sh) file in the data-tools/use_case repository.

<br>

<strong>net_type = road_link, theme = tn</strong>
| country                        | country_code | distance | 
|--------------------------------|--------------|----------|
| The Netherlands                | nl           | 5        |
| Belgium                        | be           | 5        |
| France                         | fr           | 5        |
| Suisse                         | ch           | 5        |
| Luxembourg                     | lu           | 5        |

<br>

<strong>net_type = railway_link, theme = tn</strong>
| country                        | country_code | distance |
|--------------------------------|--------------|----------|
| The Netherlands                | nl           | 5        |
| Belgium                        | be           | 5        |
| France                         | fr           | 5        |
| Suisse                         | ch           | 5        |
| Luxembourg                     | lu           | 5        |

<br>

<strong>net_type = watercourse_link, theme = hy</strong>
| country                        | country_code | distance |
|--------------------------------|--------------|----------|
| The Netherlands                | nl           | 5        |
| Belgium                        | be           | 5        |
| France                         | fr           | 5        |
| Suisse                         | ch           | 5        |
| Luxembourg                     | lu           | 5        |

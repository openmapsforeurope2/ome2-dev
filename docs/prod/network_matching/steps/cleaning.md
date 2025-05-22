
# Cleaning step

The "cleaning" step consists in deleting objects located outside of the country's extene and more than a certain distance away from its international boundaries. The default distance used is 5 meters.

This means that in OME2, we consider that objects provided by a country and located less than 5 meters away for the international boundary (even if they are in the neighbouring country's extent) can be kept. Objects located in the neighbouring country and more than 5 meters away from the international boundary are deleted by the cleaning step.

Once new data has been integrated in the OME2 database and once the OME2 version of its international boundaries have been defined, the cleaning step needs to be run to delete the relevant objects.

```
python3 script/clean.py -c conf.json -d <distance> -T <theme> -t <net_type>_w <country_code>
```

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

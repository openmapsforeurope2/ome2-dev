# User guide for the production of the AU (Administrative units) theme

## Step 1: model conversion
When a new AU dataset is received for a country, the first step consists in implementing the model conversion parameter file, then launch the model conversion itself.
See [add link]
As a result, the administrative tables for each relevant level for the country will be filled:
* au.administrative_unit_area_1
* au.administrative_unit_area_2
* au.administrative_unit_area_3
* au.administrative_unit_area_4
* au.administrative_unit_area_5
* au.administrative_unit_area_6

## Step 2: generate OME2 international boundaries with neighbouring countries


## Step 3: edge-match administrative units at the lowest level



## Step 4: edge-match administrative units at all other levels
Upper level administrative units are recreated by merging AUs at a lower level, using the [au_merging](https://github.com/openmapsforeurope2/au_merging) tool on each level successively. 

Please note that the last complete level should be used as reference for merging. For instance, in France, level 5 does not cover the whole territory. Therefore, au.administrative_unit_area_4 will be recreated using au.administrative_unit_area_6 as reference:
<pre>ome2_au_merging --c path/to/config/epg_parameters_merging_ng.ini --s au_administrative_unit_area_6 --t administrative_unit_area_4_w --cc fr</pre>

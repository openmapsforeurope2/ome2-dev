## Cleaning step (10)
### 1) Extract objects around a country's boundaries for cleaning: 

<u>The Netherlands:</u>
~~~
python3 script/border_extraction.py -c conf.json -T tn -t road_link -d 4000 nl '#'
python3 script/border_extraction.py -c conf.json -T tn -t railway_link -d 4000 nl '#'
python3 script/border_extraction.py -c conf.json -T hy -t watercourse_link -d 4000 nl '#'
~~~

<u>Belgium:</u>
~~~
python3 script/border_extraction.py -c conf.json -T tn -t road_link -d 4000 be '#'
python3 script/border_extraction.py -c conf.json -T tn -t railway_link -d 4000 be '#'
python3 script/border_extraction.py -c conf.json -T hy -t watercourse_link -d 4000 be '#'
~~~

<u>France:</u>

~~~
python3 script/border_extraction.py -c conf.json -T tn -t road_link -d 3000 fr '#'

ATTENTION!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
voir si pour avoir les zone "in dispute", plutot ecrire :
python3 script/border_extraction.py -c conf.json -T tn -t road_link -B international -d 3000 fr


// or
python3 script/border_extraction.py -c conf.json -T tn -t road_link -b false -B international -d 3000 fr
python3 script/border_extraction.py -c conf.json -T tn -t road_link -b ad -d 3000 -n fr
python3 script/border_extraction.py -c conf.json -T tn -t road_link -b mc -d 3000 -n fr
python3 script/border_extraction.py -c conf.json -T tn -t road_link -b lu -d 3000 -n fr
python3 script/border_extraction.py -c conf.json -T tn -t road_link -b it -d 3000 -n fr
python3 script/border_extraction.py -c conf.json -T tn -t road_link -b es -d 3000 -n fr
python3 script/border_extraction.py -c conf.json -T tn -t road_link -b ch -d 3000 -n fr
python3 script/border_extraction.py -c conf.json -T tn -t road_link -b de -d 3000 -n fr
python3 script/border_extraction.py -c conf.json -T tn -t road_link -b be -d 3000 -n fr

python3 script/border_extraction.py -c conf.json -T tn -t railway_link -b false -B international -d 3000 fr
python3 script/border_extraction.py -c conf.json -T tn -t railway_link -b ad -d 4000 -n fr
python3 script/border_extraction.py -c conf.json -T tn -t railway_link -b mc -d 4000 -n fr
python3 script/border_extraction.py -c conf.json -T tn -t railway_link -b lu -d 4000 -n fr
python3 script/border_extraction.py -c conf.json -T tn -t railway_link -b it -d 4000 -n fr
python3 script/border_extraction.py -c conf.json -T tn -t railway_link -b es -d 4000 -n fr
python3 script/border_extraction.py -c conf.json -T tn -t railway_link -b ch -d 4000 -n fr
python3 script/border_extraction.py -c conf.json -T tn -t railway_link -b de -d 4000 -n fr
python3 script/border_extraction.py -c conf.json -T tn -t railway_link -b be -d 4000 -n fr

python3 script/border_extraction.py -c conf.json -T hy -t watercourse_link -b false -B international -d 3000 fr
python3 script/border_extraction.py -c conf.json -T hy -t watercourse_link -b ad -d 3000 -n fr
python3 script/border_extraction.py -c conf.json -T hy -t watercourse_link -b mc -d 3000 -n fr
python3 script/border_extraction.py -c conf.json -T hy -t watercourse_link -b lu -d 3000 -n fr
python3 script/border_extraction.py -c conf.json -T hy -t watercourse_link -b it -d 3000 -n fr
python3 script/border_extraction.py -c conf.json -T hy -t watercourse_link -b es -d 3000 -n fr
python3 script/border_extraction.py -c conf.json -T hy -t watercourse_link -b ch -d 3000 -n fr
python3 script/border_extraction.py -c conf.json -T hy -t watercourse_link -b de -d 3000 -n fr
python3 script/border_extraction.py -c conf.json -T hy -t watercourse_link -b be -d 3000 -n fr
~~~

<u>Suisse:</u>
~~~
python3 script/border_extraction.py -c conf.json -T tn -t road_link -d 4000 ch '#'
python3 script/border_extraction.py -c conf.json -T tn -t railway_link -d 4000 ch '#'
python3 script/border_extraction.py -c conf.json -T hy -t watercourse_link -d 4000 ch '#'
~~~

<u>Luxembourg:</u>
~~~
python3 script/border_extraction.py -c conf.json -T tn -t road_link -d 4000 lu '#'
python3 script/border_extraction.py -c conf.json -T tn -t railway_link -d 4000 lu '#'
python3 script/border_extraction.py -c conf.json -T tn -t watercourse_link -d 4000 lu '#'
~~~

### 2) Clean (delete) objects outside border - (to be run from the data-tools project directory):

<u>The Netherlands:</u>
~~~
python3 script/clean.py -c conf.json -d 5 -T tn -t road_link_w nl
python3 script/clean.py -c conf.json -d 5 -T tn -t railway_link_w nl
python3 script/clean.py -c conf.json -d 5 -T hy -t watercourse_link_w nl
~~~

<u>Belgium:</u>
~~~
python3 script/clean.py -c conf.json -d 5 -T tn -t road_link_w be
python3 script/clean.py -c conf.json -d 5 -T tn -t railway_link_w be
python3 script/clean.py -c conf.json -d 5 -T hy -t watercourse_link_w be
~~~

<u>France:</u>
~~~
python3 script/clean.py -c conf.json -d 5 -T tn -t road_link_w fr
python3 script/clean.py -c conf.json -d 5 -T tn -t railway_link_w fr
python3 script/clean.py -c conf.json -d 5 -T hy -t watercourse_link_w fr
~~~

<u>Suisse:</u>
~~~
python3 script/clean.py -c conf.json -d 5 -T tn -t road_link_w ch
python3 script/clean.py -c conf.json -d 5 -T tn -t railway_link_w ch
python3 script/clean.py -c conf.json -d 5 -T hy -t watercourse_link_w ch
~~~

<u>Luxembourg:</u>
~~~
python3 script/clean.py -c conf.json -d 5 -T tn -t railway_link_w lu
~~~

### 3) Integrate modifications in the main table and working history table:
~~~
python3 script/integrate.py -c conf.json -T tn -t road_link -s 10
python3 script/integrate.py -c conf.json -T tn -t railway_link -s 10
python3 script/integrate.py -c conf.json -T hy -t watercourse_link -s 10
~~~


## Matching step (20)
### 1) Extract objects on the border between two neighbouring countries for matching:
~~~
python3 script/border_extraction.py -c conf.json -T tn -t road_link -d 1000 be fr
python3 script/border_extraction.py -c conf.json -T tn -t railway_link -d 1000 be fr
python3 script/border_extraction.py -c conf.json -T hy -t watercourse_link -d 1000 be fr
~~~

~~~
python3 script/border_extraction.py -c conf.json -T hy -t watercourse_area -d 1000 be fr
python3 script/border_extraction.py -c conf.json -T hy -t standing_water -d 1000 be fr
~~~

### 2) Match
~~~
./bin/net_matching --c ./data/config/epg_parameters.ini --T tn --cc be#lu
~~~

### 3) Integrate modifications in the main table and working history table:
~~~
python3 script/integrate.py -c conf.json -T tn -t road_link -s 20
~~~


## AU matching (30)
### 1) Extract objects around a country's boundaries for matching:

<u>The Netherlands:</u>
~~~
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_3 -d 1000 nl '#'
~~~

<u>Belgium:</u>

Example of an extraction around boundaries with only one neighbouring country:
~~~
python3 script/border_extraction.py exit-c conf.json -T au -t administrative_unit_area_5 -b nl -d 1000 be
~~~

Example of an extraction around boundaries with several neighbouring countries:
~~~
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_5 -b nl -d 1000 be
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_5 -b de -d 1000 -n be
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_5 -b lu -d 1000 -n be
~~~

Example of an extraction around all boundaries:
~~~
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_5 -d 1000 be '#'
~~~

<u>France:</u>
~~~
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_6 -d 1000 fr '#'
~~~

### 2) Matching
Copy boundary tables and country outlines in the public schema: 
~~~
python3 script/copy_table.py -c conf.json au.administrative_unit_area_1 ib.international_boundary_line
~~~

Run process:

<u>The Netherlands:</u>
~~~
bin/au_matching --c data/config/epg_parameters.ini --t work.administrative_unit_area_3_w --cc nl
~~~

<u>Belgium:</u>
~~~
bin/au_matching --c data/config/epg_parameters.ini --t work.administrative_unit_area_5_w --cc be
~~~

<u>France:</u>
~~~
bin/au_matching --c data/config/epg_parameters.ini --t work.administrative_unit_area_6_w --cc fr
~~~

### 3) Integrate modifications in the main table and working history (wh) table
Before running the integrate, check in the log file whether invalid polygons have been generated by the matching process. If there are some, correct them in QGIS.

<u>The Netherlands:</u>
~~~
python3 script/integrate.py -c conf.json -T au -t administrative_unit_area_3 -s 30
~~~

<u>Belgium:</u>
~~~
python3 script/integrate.py -c conf.json -T au -t administrative_unit_area_5 -s 30
~~~

<u>France:</u>
~~~
python3 script/integrate.py -c conf.json -T au -t administrative_unit_area_6 -s 30
~~~


## Administrative merging (30)
### Level 5)
#### 1) Extract objects around a country's boundaries
<u>France:</u>
~~~
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_5 -d 1000 fr '#'
~~~

#### 2) Merging
Copy lower level administrative unit table in the public schema:
~~~
python3 script/copy_table.py -c conf.json au.administrative_unit_area_6
~~~

Run process:

<u>France:</u>
~~~
bin/au_merging --c data/config/epg_parameters.ini --s au_administrative_unit_area_6 --t administrative_unit_area_5_w --cc fr
~~~

#### 3)  Integrate modifications in the main table and working history (wh) table
~~~
python3 script/integrate.py -c conf.json -T au -t administrative_unit_area_5 -s 30
~~~


### Level 4)
#### 1) Extract objects around a country's boundaries
<u>Belgium:</u>
~~~
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_4 -d 1000 be '#'
~~~

<u>France:</u>
~~~
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_4 -d 1000 fr '#'
~~~

#### 2) Merging
Copy lower level administrative unit table in the public schema:

<u>Belgium:</u>
~~~
python3 script/copy_table.py -c conf.json au.administrative_unit_area_5
~~~

<u>France:</u>
~~~
python3 script/copy_table.py -c conf.json au.administrative_unit_area_6
~~~

Run process:

<u>Belgium:</u>
~~~
bin/au_merging --c data/config/epg_parameters.ini --s prod.administrative_unit_area_5 --t work.administrative_unit_area_4_w --cc be
~~~

<u>France:</u>
~~~
bin/au_merging --c data/config/epg_parameters.ini --s prod.administrative_unit_area_6 --t work.administrative_unit_area_4_w --cc fr
~~~

#### 3)  Integrate modifications in the main table and working history (wh) table
Before running the integrate, check in the log file whether invalid polygons have been generated by the matching process. If there are some, correct them in QGIS.

~~~
python3 script/integrate.py -c conf.json -T au -t administrative_unit_area_4 -s 30
~~~

### Level 3)
#### 1) Extract objects around a country's boundaries

<u>Belgium:</u>
~~~
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_3 -d 1000 be '#'
~~~

<u>France:</u>
~~~
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_3 -d 1000 fr '#'
~~~

#### 2) Matching
Copy lower level administrative unit table in the public schema:

<u>Belgium, France:</u>
~~~
python3 script/copy_table.py -c conf.json au.administrative_unit_area_4
~~~

Run process:

<u>Belgium:</u>
~~~
bin/au_merging --c data/config/epg_parameters.ini --s prod.administrative_unit_area_4 --t work.administrative_unit_area_3_w --cc be
~~~

<u>France:</u>
~~~
bin/au_merging --c data/config/epg_parameters.ini --s prod.administrative_unit_area_4 --t work.administrative_unit_area_3_w --cc fr
~~~

#### 3)  Integrate modifications in the main table and working history (wh) table
Before running the integrate, check in the log file whether invalid polygons have been generated by the matching process. If there are some, correct them in QGIS.

~~~
python3 script/integrate.py -c conf.json -T au -t administrative_unit_area_3 -s 30
~~~

### Level 2)
#### 1) Extract objects around a country's boundaries
<u>The Netherlands:</u>
~~~
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_2 -d 1000 nl '#'
~~~

<u>Belgium:</u>
~~~
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_2 -d 1000 be '#'
~~~

<u>France:</u>
~~~
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_2 --d 1000 fr '#'
~~~

#### 2) Matching
Copy lower level administrative unit table in the public schema:

<u>The Netherlands, Belgium, France:</u>
~~~
python3 script/copy_table.py -c conf.json au.administrative_unit_area_3
~~~

Run process:

<u>The Netherlands:</u>
~~~
bin/au_merging --c data/config/epg_parameters.ini --s prod.administrative_unit_area_3 --t work.administrative_unit_area_2_w --cc nl
~~~

<u>Belgium:</u>
~~~
bin/au_merging --c data/config/epg_parameters.ini --s prod.administrative_unit_area_3 --t work.administrative_unit_area_2_w --cc be
~~~

<u>France:</u>
~~~
bin/au_merging --c data/config/epg_parameters.ini --s prod.administrative_unit_area_3 --t work.administrative_unit_area_2_w --cc fr
~~~

#### 3)  Integrate modifications in the main table and working history (wh) table
Before running the integrate, check in the log file whether invalid polygons have been generated by the matching process. If there are some, correct them in QGIS.

~~~
python3 script/integrate.py -c conf.json -T au -t administrative_unit_area_2 -s 30
~~~

### Level 1)
#### 1) Extract objects around a country's boundaries
<u>The Netherlands:</u>
~~~
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_1 -d 1000 nl '#'
~~~

<u>Belgium:</u>
~~~
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_1 -d 1000 be '#'
~~~

<u>France:</u>
~~~
python3 script/border_extraction.py -c conf.json -T au -t administrative_unit_area_1 -d 1000 fr '#'
~~~

#### 2) Matching
Copy lower level administrative unit table in the public schema:

<u>The Netherlands, Belgium, France:</u>
~~~
python3 script/copy_table.py -c conf.json au.administrative_unit_area_2
~~~

Run process:

<u>The Netherlands:</u>
~~~
bin/au_merging --c data/config/epg_parameters.ini --s prod.administrative_unit_area_2 --t work.administrative_unit_area_1_w --cc nl
~~~

<u>Belgium:</u>
~~~
bin/au_merging --c data/config/epg_parameters.ini --s prod.administrative_unit_area_2 --t work.administrative_unit_area_1_w --cc be
~~~

<u>France:</u>
~~~
bin/au_merging --c data/config/epg_parameters.ini --s prod.administrative_unit_area_2 --t work.administrative_unit_area_1_w --cc fr
~~~

#### 3)  Integrate modifications in the main table and working history (wh) table
~~~
python3 script/integrate.py -c conf.json -T au -t administrative_unit_area_1 -s 30
~~~


## Rollback
Go back to step N (cancel modifications including those performed by step N):
~~~
python3 script/revert.py -c conf.json -T hy -t watercourse_link -s 10
python3 script/revert.py -c conf.json -T tn -t road_link -s 10
python3 script/revert.py -c conf.json -T tn -t railway_link -s 10
python3 script/revert.py -c conf.json -T au -t administrative_unit_area_3 -s 30
~~~



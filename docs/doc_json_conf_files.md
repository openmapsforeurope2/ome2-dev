# How to fill a json configuration file for the model conversion tool?

### General parameters
~~~
    "country_code": "fi",
    "source_srid": "3416",
    "target_srid": "3035",
    "target_country_field": "country",
~~~

~~~
    "country_code": "fr",
    "country_code_list": ["fr","gf","gu","gp","mq","re","yt","bl","mf","pm"],
    "source_srid": "CASE gcms_territoire WHEN 'FXX' THEN 2154 WHEN 'GLP' THEN 4559 WHEN 'GUF' THEN 2972 WHEN 'H_T' THEN 4326 WHEN 'MTQ' THEN 4559 WHEN 'MYT' THEN 4471 WHEN 'REU' THEN 2975 WHEN 'SPM' THEN 4467 END",
    "target_srid": "3035",
    "target_country_field": "country",
~~~

![under_construction](images/under_construction.png)

# road_link matching steps sequencing

## cleaning
### 1) Extract objects around a country's boundaries for cleaning: 
[extraction](steps/extraction)

### 2) Cleaning (delete) objects outside border - (to be run from the data-tools project directory):
[cleaning](steps/cleaning)

### 3) Integrate modifications in the main table and working history table:
[integrate](steps/integrate)

## Matching
### 1) Extract objects on the border between two neighbouring countries for matching:
[extraction](steps/extraction) with <distance> = 1000

### 2) Matching
[matching](steps/matching)

### 3) Integrate modifications in the main table and working history table:
[integrate](steps/integrate) with <step> = 20
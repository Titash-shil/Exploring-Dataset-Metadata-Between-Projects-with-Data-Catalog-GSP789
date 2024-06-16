# Exploring Dataset Metadata Between Projects with Data Catalog || [GSP789](https://www.cloudskillsboost.google/focuses/11034?parent=catalog) ||

# # Like, comment, share & Don't forget to subscribe [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN) 👍😄🤝

### Run the following Commands in CloudShell ( `Project-1` Or `NYC Bike Share Project` )

```
export PROJECT_ID_2=
```
```
export REGION=
```
```
#!/bin/bash
# Define color variables

BLACK=`tput setaf 0`
RED=`tput setaf 1`
GREEN=`tput setaf 2`
YELLOW=`tput setaf 3`
BLUE=`tput setaf 4`
MAGENTA=`tput setaf 5`
CYAN=`tput setaf 6`
WHITE=`tput setaf 7`

BG_BLACK=`tput setab 0`
BG_RED=`tput setab 1`
BG_GREEN=`tput setab 2`
BG_YELLOW=`tput setab 3`
BG_BLUE=`tput setab 4`
BG_MAGENTA=`tput setab 5`
BG_CYAN=`tput setab 6`
BG_WHITE=`tput setab 7`

BOLD=`tput bold`
RESET=`tput sgr0`
#----------------------------------------------------start--------------------------------------------------#

echo "${BG_MAGENTA}${BOLD}Starting Execution${RESET}"

gcloud data-catalog tag-templates create new_york_datasets --display-name="New York Datasets" --location=$REGION --field=id=contains_pii,display-name="Contains PII",type='enum(None|Birth date|Gender|Geo location)' --field=id=data_owner_team,display-name="Data Owner Team",type='enum(Marketing|Data Science|Sales|Engineering)',required=TRUE

gcloud config set project $PROJECT_ID_2

bq query --use_legacy_sql=false \
'SELECT
  contributing_factor_vehicle_1 AS collision_factor,
  COUNT(*) AS num_collisions
FROM
  `new_york_mv_collisions.nypd_mv_collisions`
WHERE
  contributing_factor_vehicle_1 != "Unspecified"
  AND contributing_factor_vehicle_1 != ""
GROUP BY
  collision_factor
ORDER BY
  num_collisions DESC
LIMIT 10;'

echo "${BLUE}${BOLD}NOW${RESET}" "${PURPLE}${BOLD}FOLLOW${RESET}" "${YELLOW}${BOLD}VIDEO'S INSTRUCTIONS${RESET}"

#-----------------------------------------------------end----------------------------------------------------------#
```

### Run the following Query in `BigQuery` ( `Project-1` Or `NYC Bike Share Project` )

```
WITH unknown AS (
  SELECT
    gender,
    CONCAT(start_station_name, " to ", end_station_name) AS route,
    COUNT(*) AS num_trips
  FROM
    `new_york_citibike.citibike_trips`
  WHERE gender = 'unknown'
  GROUP BY
    gender,
    start_station_name,
    end_station_name
  ORDER BY
    num_trips DESC
  LIMIT 5
)

, female AS (
  SELECT
    gender,
    CONCAT(start_station_name, " to ", end_station_name) AS route,
    COUNT(*) AS num_trips
  FROM
    `new_york_citibike.citibike_trips`
  WHERE gender = 'female'
  GROUP BY
    gender,
    start_station_name,
    end_station_name
  ORDER BY
    num_trips DESC
  LIMIT 5
)

, male AS (
  SELECT
    gender,
    CONCAT(start_station_name, " to ", end_station_name) AS route,
    COUNT(*) AS num_trips
  FROM
    `bigquery-public-data.new_york_citibike.citibike_trips`
  WHERE gender = 'male'
  GROUP BY
    gender,
    start_station_name,
    end_station_name
  ORDER BY
    num_trips DESC
  LIMIT 5
)

SELECT * FROM unknown
UNION ALL
SELECT * FROM female
UNION ALL
SELECT * FROM male;
```

# Congratulations ..!! You completed the lab shortly..😃💯

# *Well done..!* 👏

# Thank you for visiting.... :) 🗯️

# [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN)

# Taxi Service Web App
**Skills:** 
- Command Line
- SQL
- PostgreSQL
- Databases

## Overview
For this project, I analyzed the operational aspects of taxi services in Chicago, focusing on the efficiency of taxi distribution among various cab companies and the impact of weather conditions on taxi operations. The primary goal was to understand the adequacy of taxi availability and explore any correlation between weather patterns and taxi trips.

This project required me to use the console to access a remote server. First, I worked with files and directories and then with a taxi service's database.

## Tasks 
### Example #1
A bug was detected in the system. It appeared twice: first on December 30, 2019, and then again on December 31, 2019. The developers want to investigate the bug by examining logs that contain `400` and `500` error codes. For now, they only want to focus on the first day. My task was to find the logs from the first day, save them in a single file, and split the results into two separate files based on the error code.

**My Queries**

To select logs for the specified periods:
```
grep ' [45]00 ' ~/logs/2019/12/apache_2019-12-30.txt > ~/bug1/main.txt
```
To put logs from the main.txt file into the 400.txt and 500.txt files:
```
grep ' 400 ' ~/bug1/main.txt > ~/bug1/events/400.txt
grep ' 500 ' ~/bug1/main.txt > ~/bug1/events/500.txt
```
### Example #2
According to the plan, 10,550 cars were supposed to enter the service line, which should have covered the user demand. However, the team received many complaints that there were not enough available cars. My task was to find out how many taxis entered the line and generate a list of companies with fewer than 100 cars.

**My Queries**

To find the number of cars:
```
SELECT 
COUNT(DISTINCT vehicle_id) AS number_of_cars 
FROM cabs;
```
To generate the list of companies with fewer than 100 cars:
```
SELECT
    company_name,
    COUNT(vehicle_id) AS cnt
FROM
    cabs
GROUP BY
    company_name
HAVING
    COUNT(vehicle_id) < 100
ORDER BY
    cnt DESC;
```

## Findings

### Taxi Fleet Analysis:
- The number of taxis in service was below the planned number.
- Several companies had fewer than 100 cars, indicating potential service gaps.
### Weather and Taxi Operations:
- Clear patterns showing the impact of weather on taxi usage.
- Certain weather conditions, like heavy rain, correlated with a surge in taxi demand.

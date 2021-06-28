# Surfs up Challenge
## June vs December Temperature Analysis

## Overview

The purpose of this analysis is to help W. Avy to analyse temperature data for June and December in Oahu using SQLAlchemy and Python. 
The main objective of this analysis is to help W. Avy determine if the surf and ice cream shop business is sustainable year round. 

## Results

After performing this analysis we can observe that the temperatures in June and December have these key differences: 

1) There is a 9F degree difference between June and December on the min observed temperature
2) There is only a 2F degree difference between June and December on the max observed tempreature
3) There is only a 3F degree difference between the average temperatures between June and December. 


## Summary

### High level results: 

Historically, it seems like there is really not a lot of variation between the temperatures across these two months.

#### June 

| Tempreatures Observed|
|-------|--------------|
| count	| 1700.000000  |
| mean	| 74.944118    |
| std	  | 3.257417     |
| min	  | 64.000000    |
| 25%	  | 73.000000    |
| 50%	  | 75.000000    |
| 75%	  | 77.000000    |
| max	  | 85.000000    |


#### December

| Tempreatures Observed|
|-------|--------------|
| count	| 1517.000000  |
| mean	| 71.041529    |
| std	  | 3.745920     |
| min	  | 56.000000    |
| 25%	  | 69.000000    |
| 50%	  | 71.000000    |
| 75%	  | 74.000000    |
| max	  | 83.000000    |

Additional queries: 
1) Breaking out the average observed temps by year by using the following queries: 
  - For December
  ```python
    session.query(extract('year',Measurement.date),func.avg(Measurement.tobs))\
    .filter(extract('month',Measurement.date) == '12').group_by(extract('year',Measurement.date)).all()
  ```
  - For June
  ```python
     session.query(extract('year',Measurement.date),func.avg(Measurement.tobs))\
    .filter(extract('month',Measurement.date) == '12').group_by(extract('year',Measurement.date)).all()
  ```
3) Bringing additional information per station to observe if maybe there was any important variations by station
  - For December
  ```python
    session.query(Measurement.station,func.avg(Measurement.prcp),func.avg(Measurement.tobs))\
    .filter(extract('month',Measurement.date) == '12').group_by(Measurement.station).all()
  ```
  - For June
  ```python
    session.query(Measurement.station,func.avg(Measurement.prcp),func.avg(Measurement.tobs))\
    .filter(extract('month',Measurement.date) == '6').group_by(Measurement.station).all()
  ```

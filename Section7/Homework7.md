# Section 7 Homework

## 7.1

### 1. Using EVregistry, Write a query to select the ModelYear, Make, and Model off all of the vehicles in the registry.

SELECT ModelYear, Make, Model
FROM EVRegistry

### 2. Using the EVRegistry table, Write a query that lists all of the unique types of EV's. your reult set should have one column, ElectricVehicleType.

SELECT DISTINCT ElectricVehicleType
FROM EVRegistry

### 3. Using the EVRegistry, Write a query that shows all of the information on Battery Electric Vehicles (BEV) that are in the registry.

SELECT *
FROM evRegistry
WHERE ElectricVehicleType = "Battery Electric Vehicle (BEV)" 

### 4. Using the EVRegistry, wirte a query that returns the Make and Model of all of the EV's that have a BaseMSRP between 20000 and 35000?

SELECT Make, Model
FROM evRegistry
WHERE BaseMSRP BETWEEN 20000 and 35000

## 7.2

### 5. Using EVRegistry, write a query to find a record where the City attribute is NULL. Return all of the available columns.
SELECT * 
FROM evRegistry
WHERE City IS NULL;

### 6. Write a query to find the make, model, and ElectricVehicleType where the VIN number has that ends in '3E1EA1J'.
SELECT Make, Model, ElectricVehicleType
FROM evRegistry
WHERE VIN LIKE '%3E1EA1J'

### 7. Select the ModelYear, make, model, ElectricVehicleType, and range of the Tesla vehicles or cheverolet vehicles in the registry. Order the result set by Make and Model year in from newest to oldest.

SELECT ModelYear, Make, Model, ElectricVehicleType, ElectricRange
FROM evRegistry
WHERE Make IN ('TESLA', 'CHEVROLET')
ORDER BY Make, ModelYear ASC;

### 8. Using EVCharging, Write a query to find out how many many times those stations were used. Order them by the most used to the least used and limit the output to 5 records.

SELECT stationId, COUNT(*) AS 'count_of_stationId'
FROM EVCharging
GROUP BY stationId
ORDER BY 'count_of_stationId' DESC
LIMIT 5;

### (I am unable to get the stations to order by most to least)

### 9. Using EVCharging, For the folks who charged longer than 0.5 hours, show the min and max of the charging time for each user. Your output columns should be userid, minTime, and maxTime. Order this result set by the last two columns respectively.

SELECT userId, MIN(chargeTimeHrs) AS minTime, MAX(chargeTimeHrs) AS maxTime
FROM EVCharging
WHERE chargeTimeHrs > 0.5
group by userId
LIMIT 2

### (is this supposed to be ordered by DESC? If so, the code is not working for me)

### 10. Using EVCharging, Which day of the week has the highest average charging time? Round the answer to 2 decimal points.

SELECT weekday, round(AVG(chargeTimeMins),2) AS 'avgchargetime'
FROM EVCharging
group by weekday
order by 'avgchargetime' DESC
 LIMIT 1;


### 11. Using, EV charging, Find the total power consumed from charging EV's by each User. Return the userId and name the calculated column, totalPower. Round the answer to 2 deciaml points and list the out put in highest to lowest order. Limit the order to the top 15 users.

SELECT userId, ROUND(count(kwhTotal),2) as 'totalpower'
FROM EVCharging
GROUP BY userId
ORDER BY 'totalpower' DESC
LIMIT 15;

(same issue with DESC)

### 12. Using dimfacility and factCharge, write a query to find out which type of facility (GROUP BY) has the most amount of charging stations. Return type Facility and name the calculated column numStation. Order the result set from highest to lowest number of charging stations.

SELECT dimFacility. typeFacility, COUNT(factCharge.facilityID) as 'numStation'
FROM dimFacility
INNER JOIN factCharge on dimFacility. FacilityKey = factCharge.facilityID
group by typeFacility
ORDER BY 'numStation' DESC;

### 13. 13In your own words, Briefly explain Primary Keys and Foreign Keys.

## Foreign and primary keys
## Primary: uniquely identifies each record that exists in table
##  * Never NULL values
## Foreign: the foreign key in one table refers to the primary key  in a “connected” table
### * Foreign key designation helps prevent any action that could destroy the link between the two tables


### 14. Using EV Charging, For the folks who charged longer than one hour, show the min and max of the charging time for each user. Your output columns should be userid, minTime, and maxTime. Order this result set by the last two columns respectively. HINT: USE HAVING

 select userId,  min(chargeTimeHrs ), max(chargeTimeHrs )
 FROM EVCharging
 group by userId
 HAVING chargeTimeHrs > 1
# SECTION 07 HW 

<br>

# 7.1 HW Questions 

1. Using EVregistry, Write a query to select the `ModelYear`, `Make`, and `Model` off all of the vehicles in the registry.
```SQL
SELECT ModelYear, Make, Model
FROM EVRegistry
```
2. Using the EVRegistry table, Write a query that lists all of the unique types of EV's. your reult set should have one column, `ElectricVehicleType`. 
```SQL
SELECT DISTINCT ElectricVehicleType
FROM EVRegistry
```
3. Using the EVRegistry, Write a query that shows all of the information on Battery Electric Vehicles (BEV) that are in the registry. 
```SQL
SELECT *
FROM EVRegistry
WHERE ElectricVehicleType LIKE '%BEV%';
```
4. Using the EVRegistry, wirte a query that returns the `Make` and `Model` of all of the EV's that have a BaseMSRP between 20000 and 35000?  
```SQL
SELECT Make, Model
FROM EVRegistry
WHERE BaseMSRP BETWEEN 20000 AND 35000;
```


# 7.2 HW Questions 

1. Using EVRegistry, write a query to find a record  where the `City` attribute is NULL. Return all of the available columns. 
```SQL
SELECT *
FROM EVRegistry
WHERE City IS NULL;
```
2. Write a query to find the `make`, `model`, and `ElectricVehicleType` where the VIN number has  that ends in '3E1EA1J'.
```SQL
SELECT Make, Model, ElectricVehicleType
FROM EVRegistry
WHERE VIN LIKE '%3E1EA1J';
```
3. Select the `ModelYear`, `make`, `model`, `ElectricVehicleType`, and `range` of the Tesla vehicles or cheverolet vehicles in the registry. Order the result set by Make and Model year in from newest to oldest. 
```SQL
SELECT ModelYear, Make, Model, ElectricVehicleType, ElectricRange
FROM EVRegistry
WHERE Make IN ('TESLA', 'CHEVROLET')
ORDER BY Make, ModelYear DESC;
```
4. Using EVCharging, Write a query to find out how many many times those stations were used. Order them by the most used to the least used and limit the output to 5 records. 
```SQL
SELECT StationID, COUNT(*) AS UseCount
FROM EVCharging
GROUP BY StationID
ORDER BY UseCount DESC
LIMIT 5;
```
5.  Using EVCharging, For the folks who charged longer than 0.5 hours, show the min and max of the charging time for each user. Your output columns should be `userid`, `minTime`, and `maxTime`. Order this result set by the last two columns respectively. 
```SQL
SELECT
    UserID,
    MIN(chargeTimeHrs) AS minTime,
    MAX(chargeTimeHrs) AS maxTime
FROM
    EVCharging
WHERE
    chargeTimeHrs > 0.5
GROUP BY
    UserID
ORDER BY
    minTime, maxTime;
```


# 7.3 HW Questions

1. Using EVCharging, Which day of the week has the highest average charging time? Round the answer to 2 decimal points.
```SQL
SELECT
    weekday AS DayOfWeek,
    ROUND(AVG(chargeTimeHrs), 2) AS AvgChargeTime
FROM
    EVCharging
GROUP BY
    weekday
ORDER BY
    AvgChargeTime DESC
LIMIT 1;
```
2. Using, EV charging, Find the total power consumed from charging EV's by each User. Return the `userId` and name the calculated column, 
`totalPower`. Round the answer to 2 deciaml points and list the out put in highest to lowest order. Limit the order to the top 15 users. 
```SQL
SELECT
    userId,
    ROUND(SUM(kwhTotal), 2) AS totalPower
FROM
    EVCharging
GROUP BY
    userId
ORDER BY
    totalPower DESC
LIMIT 15;
```
3. Using dimfacility and factCharge, write a query to find out which type of facility (GROUP BY) has the most amount of charging stations. Return `type Facility` and name the calculated column `numStation`. Order the result set from highest to lowest number of charging stations.  
```SQL
SELECT
    df.typeFacility,
    COUNT(fc.stationId) AS numStation
FROM
    dimfacility df
JOIN
    factCharge fc ON df.FacilityKey = fc.FacilityID
GROUP BY
    df.typeFacility
ORDER BY
    numStation DESC;
```
4. In your own words, Briefly explain Primary Keys and Foreign Keys. 

`Primary keys identifies unique values in the record. Foreign keys acts like primary keys on connected table.`

5. Using EV Charging, For the folks who charged longer than one hour, show the min and max of the charging time for each user. Your output columns should be `userid`, `minTime`, and `maxTime`. Order this result set by the last two columns respectively. HINT: USE `HAVING`
```SQL
SELECT
    userId,
    MIN(chargeTimeHrs) AS minTime,
    MAX(chargeTimeHrs) AS maxTime
FROM
    EVCharging
GROUP BY
    userId
HAVING
    MAX(chargeTimeHrs) > 1
ORDER BY
    minTime, maxTime;
```

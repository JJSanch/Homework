1. Using EVregistry, Write a query to select the ModelYear, Make, and Model off all of the vehicles in the registry.

        SELECT  ModelYear, Make,  Model
        from EVRegistry

2. Using the EVRegistry table, Write a query that lists all of the unique types of EV's. your result set should have one column, ElectricVehicleType.

        SELECT DISTINCT ElectricVehicleType
        from EVRegistry


3.  Using the EVRegistry, Write a query that shows all of the information on Battery Electric Vehicles (BEV) that are in the registry.

        SELECT *
        FROM EVRegistry
        WHERE ElectricVehicleType LIKE '%BEV%'

4.  Using the EVRegistry, write a query that returns the Make and Model of all of the EV's that have a BaseMSRP between 20000 and 35000?

          SELECT MAKE, Model, BaseMSRP
          FROM EVRegistry  
          WHERE BaseMSRP BETWEEN 20000 AND 35000; 
        




     
7.2 QUESTIONS

-- 1Using EVRegistry, write a query to find a record where the City attribute is NULL. Return all of the available columns.

SELECT *
from EVRegistry
WHERE City is NULL
     

-- 2 Write a query to find the make, model, and ElectricVehicleType where the VIN number has that ends in '3E1EA1J'.

SELECT make,Model,ElectricVehicleType
FROM EVRegistry
WHERE VIN like '%3E1Ea1J'

      
     
3.  Select the ModelYear, make, model, ElectricVehicleType, and range of the Tesla vehicles or cheverolet vehicles in the registry. Order the result set by Make and Model year in from newest to oldest.

SELECT Make,Model,ElectricVehicleType, ModelYear, ElectricRange
FROM EVRegistry
ORDER BY ModelYear;
      

--4 Using EVCharging, Write a query to find out how many many times those stations were used. Order them by the most used to the least used and limit the output to 5 records.

SELECT stationId, chargeTimeHrs
FROM EVCharging
ORDER BY chargeTimeHrs DESC LIMIT 5;



     

-- 5 Using EVCharging, For the folks who charged longer than 0.5 hours, show the min and max of the charging time for each user. Your output columns should be userid, minTime, and maxTime. Order this result set by the last two columns respectively.
SELECT
	
SELECT userId, min(chargeTimeHrs) as 'minTime', max(chargeTimeHrs) as 'maxTime'
FROM EVCharging
WHERE chargeTimeHrs > 0.5 
GROUP BY userId
ORDER BY 2, 3


7.3 questions

    - 1 Using EVCharging, Which day of the week has the highest average charging time? Round the answer to 2 decimal points.

SELECT weekday, ROUND(AVG(chargeTimeHrs),2) AS 'HighestAvgDay'
FROM EVCharging
GROUP by weekday
ORDER by 2 DESC
LIMIT 1

     

-- 2 Using, EV charging, Find the total power consumed from charging EV's by each User. Return the userId and name the calculated column, totalPower. Round the answer to 2 deciaml points and list the out put in highest to lowest order. Limit the order to the top 15 users.

SELECT  userId, ROUND(SUM(kwhTotal) , 2)as 'totalPower'
FROM EVCharging
GROUP BY userId
ORDER by 2 DESC
LIMIT 15


     
3. Using dimfacility and factCharge, write a query to find out which type of facility (GROUP BY) has the most amount of charging stations. Return type Facility and name the calculated column numStation. Order the result set from highest to lowest number of charging stations.

SELECT df.FacilityKey, df.typeFacility, COUNT(DISTINCT fc.stationId) as 'numStations'
FROM dimFacility df
INNER JOIN factCharge fc
on df.FacilityKey = fc. facilityID
group by df.FacilityKey
order by 3 DESC

4.  In your own words, Briefly explain Primary Keys and Foreign Keys.

Primary key is a unique identifier that is specific to one row in a table.  Foreign key is a unique identifier used to be identify a row from a differrent table within another table.

5.  Using EV Charging, For the folks who charged longer than one hour, show the min and max of the charging time for each user. Your output columns should be userid, minTime, and maxTime. Order this result set by the last two columns respectively. HINT: USE HAVING

SELECT userId, min(chargeTimeHrs) as 'minTime', max(chargeTimeHrs) as 'maxTime'
FROM EVCharging
GROUP by userId
HAVING chargeTimeHrs > 1
ORDER by 2,3
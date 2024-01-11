# SQL-demonstration

--1. Perform the following queries on "Locations" table:
--a. select all locations that have the capacity between 200 and 1000 persons

SELECT 
Locations,
Capacity
FROM Locations
WHERE Capacity BETWEEN 200 AND 1000;

--b. select all locations that have "a" in their name

SELECT 
Locations,
LocationName
FROM Locations
where LocationName like '%a%'

--c. Select all locations that are not in Cluj-Napoca
SELECT 
City
FROM Locations
WHERE City <>'Cluj-Napoca'

--d.Select all locations that have the cost 0,500,600, are in Brasov and Cluj-Napoca, 
--and had sustain a capacity greater that 1000 persons

Select 
Locations,
Cost,
Capacity
From 
Locations
WHERE cost IN (0,500,600)
and city in ('Brasov','Cluj-Napoca')
and Capacity > 1000;

--2. Perform the following queries on "Events" table: 
--a. return the results for min, max, average based on "EventCost" column

select
 max(EventCost) as MaxEventCost, avg(EventCost) as AvgEventCost, min(EventCost) as MinEventCost
from 
 Events

--b. count how many events are associated to location 1 and 2
SELECT count(locationid) 
from events 
where (locationid = 1 or locationid=2);

--c. compute the average cost obtained from location 1
SELECT avg(EventCost)
FROM Events
WHERE (locationid = 1)


--d.	order the events based on their defined date
SELECT EventName,
EventDate
FROM Events
Order by EventDate

--e. compute the total cost associated with each location (hint grouped by)
select (locationid),sum(eventcost)
from events
group by locationid;

--3. Perform the following queries using both tables

--a.	Order location name, descending, after their associated event cost

SELECT 
LocationName,
EventCost
FROM Events,
Locations
Order by  EventCost DESC

--b. Select location name, location cost and event cost for a specific event
SELECT
LocationName,
Locations.Cost,
Events.EventCost
FROM Locations
JOIN Events ON Locations.LocationID = Events.LocationID
WHERE Events.EventID = 2

--c. Return the first 3 events (with eventName, locationname), that have the greatest event cost, 
--in alphabetical order (after their names)

SELECT
EventName,
LocationName,
EventCost
From 
Events,
Locations
ORDER BY  EventCost DESC,
EventName ASC
LIMIT 3

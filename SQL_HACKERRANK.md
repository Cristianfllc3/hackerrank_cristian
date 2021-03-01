**Test** 4**  
Select * from CITY WHERE CITY.ID = 1661;   

**Test** 5**  
SELECT DISTINCT(CITY) FROM STATION WHERE (ID%2)=0 ;  

**Test** 6**  
- SELECT (COUNT(CITY) - COUNT(DISTINCT CITY)) FROM STATION;  
- select (select count(city) from station) - (select count(distinct city) from station) from dual ;  
(mia) SELECT COUNT(*) - COUNT(DISTINCT(CITY)) FROM STATION;  

**Test** 7**
SELECT CITY, LENGTH(CITY) FROM STATION ORDER BY LENGTH(CITY),CITY ASC LIMIT 1;  
SELECT CITY, LENGTH(CITY) FROM STATION ORDER BY LENGTH(CITY) DESC LIMIT 1;  

**Test** 8
- SELECT DISTINCT city FROM station WHERE city REGEXP "^[aeiou].*";  
- SELECT DISTINCT(CITY) FROM STATION WHERE CITY RLIKE '^[aeiou]';  
- select distinct(city) from station where lower(substr(city,1,1)) in ('a','e','i','o','u');  


**Test** 9
SELECT DISTINCT CITY FROM STATION WHERE RIGHT(CITY,1) IN ('a','i','e','o','u');
SELECT DISTINCT CITY FROM STATION WHERE CITY REGEXP '[aeiou]$';

**Test** 10
SELECT DISTINCT CITY FROM STATION WHERE CITY REGEXP "^[aeiou].*" AND CITY REGEXP "[aeiou]$";  
SELECT DISTINCT CITY FROM STATION WHERE CITY REGEXP '^[aeiou].*[aeiou]$';  

**Test** 11
- SELECT DISTINCT CITY FROM STATION WHERE CITY NOT REGEXP '^[aeiou]';  
- SELECT DISTINCT CITY FROM STATION WHERE CITY REGEXP '^[^aeiou]';  
- SELECT DISTINCT CITY FROM STATION
WHERE NOT (CITY LIKE 'A%' OR  CITY  LIKE 'E%' OR CITY  LIKE 'I%' OR CITY  LIKE 'O%' OR CITY  LIKE 'U%');  

**Test** 12  
SELECT DISTINCT CITY FROM STATION WHERE CITY REGEXP '^[^aeiou].*[^aeiou]$';  
SELECT DISTINCT CITY FROM STATION WHERE CITY NOT REGEXP "^[aeiou].*" AND CITY NOT REGEXP "[aeiou]$";  
  
**Test** 13
SELECT NAME FROM STUDENTS WHERE MARKS > 75 ORDER BY RIGHT(NAME, 3), ID ASC;  
SELECT NAME FROM STUDENTS WHERE MARKS > 75 ORDER BY SUBSTRING(NAME, -3), ID ASC;  
   
**Test** 14  
SELECT NAME FROM EMPLOYEE ORDER BY NAME ASC;  

**Test** 15  
SELECT NAME FROM EMPLOYEE WHERE MONTHS<10 AND SALARY>2000 ORDER BY EMPLOYEE_ID ASC;  
  
**Test** 16  
SELECT MAX(POPULATION) - MIN(POPULATION) FROM CITY;  
   
**Test** 17  
SELECT CEIL(AVG(Salary)-AVG(REPLACE(Salary,'0',''))) FROM EMPLOYEES;  
  
**Test** 18  
SELECT MONTHS * SALARY AS EARNS, COUNT(*) FROM EMPLOYEE GROUP BY EARNS ORDER BY EARNS DESC LIMIT 1;   

**Test** 19  
- SELECT ROUND(SUM(LAT_N), 2), ROUND(SUM(LONG_W), 2) FROM STATION;  
- select round(sum(LAT_N),2) as lat, round(sum(LONG_W),2) as lon
from Station  

**Test** 20  
SELECT CASE             
            WHEN A + B > C AND B + C > A AND A + C > B THEN
                CASE 
                    WHEN A = B AND B = C THEN 'Equilateral'
                    WHEN A = B OR B = C OR A = C THEN 'Isosceles'
                    ELSE 'Scalene'
                END
            ELSE 'Not A Triangle'
        END
FROM TRIANGLES;   

**Test** 21  
select concat(name,concat('(', concat(substr(occupation,1,1),')'))) from occupations order by name;  

select concat('There are a total of',concat(' ',concat(count(occupation),concat(' ',concat(lower(occupation),'s.'))))) as total from occupations
group by occupation order by total;  

SELECT CONCAT(NAME, CONCAT ('(',SUBSTR(OCCUPATION,1,1),')')) FROM OCCUPATIONS;  
SELECT CONCAT('There are a total of ',COUNT(OCCUPATION),' ',LOWER(OCCUPATION),'s.') as T FROM OCCUPATIONS GROUP BY OCCUPATION ORDER BY T;  



**Others**  

SELECT SUM(Population) FROM City WHERE District = 'California';  
SELECT ROUND(AVG(POPULATION)) FROM CITY WHERE DISTRICT LIKE 'California';  
SELECT ROUND(AVG(POPULATION),-0.5) FROM CITY WHERE DISTRICT LIKE 'California';  
SELECT FLOOR(AVG(POPULATION)) FROM CITY;  

SELECT ROUND(SUM(LAT_N),4) FROM STATION WHERE LAT_N > 38.7880 AND LAT_N < 137.2345;  
SELECT TRUNCATE(SUM(LAT_N), 4) FROM STATION WHERE LAT_N BETWEEN 38.7880 AND 137.2345;  
SELECT ROUND(LONG_W,4) FROM STATION WHERE LAT_N < 137.2345 ORDER BY LAT_N DESC LIMIT 1;  

Manhattan distance  
p1 at (x1, y1) and p2 at (x2, y2), it is |x1 - x2| + |y1 - y2|.  
SELECT ROUND(ABS(MAX(LAT_N) - MIN(LONG_W)) + ABS(MIN(LAT_N) - MAX(LONG_W)),4) FROM STATION;  	

SELECT ROUND(SQRT(POWER(MAX(LONG_W)-MAX(LAT_N),2)+POWER(MIN(LONG_W)-MIN(LAT_N),2)),4) FROM STATION;  
SELECT
    ROUND(SQRT(
        POWER(MAX(LAT_N)  - MIN(LAT_N),  2)
      + POWER(MAX(LONG_W) - MIN(LONG_W), 2)
    ), 4)
FROM 
    STATION;  
  

SELECT DISTINCT CAST(PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY LAT_N) OVER() AS DECIMAL(10,4)) FROM STATION  

SELECT SUM(CITY.POPULATION) FROM CITY JOIN COUNTRY ON COUNTRY.CODE = CITY.COUNTRYCODE WHERE COUNTRY.CONTINENT = 'Asia';  

SELECT Name = CASE WHEN G.Grade >7 THEN S.Name ELSE NULL END, G.Grade , S.Marks FROM Students S INNER JOIN Grades G ON S.Marks >= G.Min_Mark AND S.Marks <= G.Max_Mark ORDER BY Grade DESC,Name,Marks;  

SELECT REPEAT('* ', @NUMBER := @NUMBER - 1) FROM information_schema.tables, (SELECT @NUMBER:=21) t LIMIT 20  

set @number = 21;  
select repeat('* ', @number := @number - 1) from information_schema.tables;  


DECLARE @i INT = 20
WHILE (@i > 0) 
BEGIN
   PRINT REPLICATE('* ', @i) 
   SET @i = @i - 1
END


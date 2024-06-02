# CarlaTaskOptionB

This task is completed for Rentcarla company for backend position
Firsly I used MysqlWorkbench and used draw io. Normally from ER diagram to 1NF, 1NF to 2NF and 2NF to 3NF can be drawed manually.
But with the help of MysqlWorkbench with reverse engineering method can be easily obtain 3NF form.

Firslty I created table. Then used https://www.convertcsv.com/csv-to-sql.htm to convert CSV file to SQL file for able to do insert values. And then applied queries for our database.

TASK 1

Create a schema for storing the compensation data provided in one of the available data sets. This schema should be in at least 3NF with tables for employee, role, and anything else that makes sense for the data given.

DATASET 2 3NF version 
<img width="799" alt="EgeAltinsoy3NFDS2" src="https://github.com/ege6nsoy/CarlaTaskOptionB/assets/69108759/796779b5-2cb8-4a82-b584-46e56a299689">


DATASET3 3NF version
<img width="784" alt="EgeAltinsoy3NFDS3" src="https://github.com/ege6nsoy/CarlaTaskOptionB/assets/69108759/b7f5191d-c873-48ec-99af-c54c4c655aa8">


TASK 2
Validate that you can perform the following queries. You can export the results of these queries via CSV or attach screenshots of the the output

Firsly I created a table for my DATASET 3. 
<img width="997" alt="EgeAltinsoySQLSS1" src="https://github.com/ege6nsoy/CarlaTaskOptionB/assets/69108759/5118cc18-d820-4787-a30a-4e74b2c953e0">




Secondly I wrote a sample query for testing
SELECT Employer, Location, `Job Title` FROM mytable;

whose purpose is to select specified columns from mytable table.


<img width="1440" alt="EgeAltinsoySQLSS3" src="https://github.com/ege6nsoy/CarlaTaskOptionB/assets/69108759/df896bc5-517b-4739-8afb-54c1e1a95478">

A)Average compensation of roles where the role is some kind of engineer 

SELECT AVG(`Annual Base Pay` + IFNULL(`Signing Bonus`, 0) + IFNULL(`Annual Bonus`, 0) + IFNULL(`Annual Stock Value/Bonus`, 0)) AS AverageCompensation
FROM mytable
WHERE `Job Title` LIKE '%engineer%';

code's aim is to find average salary of who has job title as engineer

<img width="1440" alt="EgeAltinsoySQLSS4" src="https://github.com/ege6nsoy/CarlaTaskOptionB/assets/69108759/b352118e-b977-40cc-a531-8288dcdac68f">

B)Average, min, and max compensation per city 


SELECT 
    
    AVG(`Annual Base Pay` + IFNULL(`Signing Bonus`, 0) + IFNULL(`Annual Bonus`, 0) + IFNULL(`Annual Stock Value/Bonus`, 0)) AS AverageCompensation,
    MIN(`Annual Base Pay` + IFNULL(`Signing Bonus`, 0) + IFNULL(`Annual Bonus`, 0) + IFNULL(`Annual Stock Value/Bonus`, 0)) AS MinCompensation,
    MAX(`Annual Base Pay` + IFNULL(`Signing Bonus`, 0) + IFNULL(`Annual Bonus`, 0) + IFNULL(`Annual Stock Value/Bonus`, 0)) AS MaxCompensation
FROM 
    mytable
GROUP BY 
    `Location`;


code's purpose is find firsly sum all incomes including signing bonus, annual bonus, annual stock value bonus
and  find  average, max, min for every city that exist in database.
<img width="1440" alt="EgeAltinsoySQLSS5" src="https://github.com/ege6nsoy/CarlaTaskOptionB/assets/69108759/bdd25bb3-1e0a-432a-998f-90579d81254e">


C)One interesting query of your choice

SELECT 
    Employer,
    SUM(`Annual Base Pay` + IFNULL(`Signing Bonus`, 0) + IFNULL(`Annual Bonus`, 0) + IFNULL(`Annual Stock Value/Bonus`, 0)) AS TotalCompensation,
    RANK() OVER (ORDER BY SUM(`Annual Base Pay` + IFNULL(`Signing Bonus`, 0) + IFNULL(`Annual Bonus`, 0) + IFNULL(`Annual Stock Value/Bonus`, 0)) DESC) AS CompensationRank
FROM 
    mytable
GROUP BY 
    Employer
ORDER BY 
    TotalCompensation DESC;

Code  works for total compensation for each employer company by summing up various components of the compensation and then ranks the employers based on the total compensation by descending.

<img width="1440" alt="EgeAltinsoySQLSS6" src="https://github.com/ege6nsoy/CarlaTaskOptionB/assets/69108759/e88b6ca2-7527-4817-b6a4-301ad990bb1b">

Task 3 
Create a quick database schema diagram
Many admin tools and clients will allow you to generate these from your schema. If not possible, just draw a super-simple diagram in MS Paint or similar tool 🎨

For this task I used draw io. Created entities and attributes and underlined primary keys for creating Schema for Dataset 2 and Dataset3.

DATASET 2
<img width="947" alt="EgeAltınsoySchemaDB2" src="https://github.com/ege6nsoy/CarlaTaskOptionB/assets/69108759/a2bfce2b-b82a-4877-aa17-c14f6526edee">

DATASET 3![EgeAltinsoySchemaDB3](https://github.com/ege6nsoy/CarlaTaskOptionB/assets/69108759/0d7d0f2d-a8ad-4fb1-92f9-68f13f9c1dc6)





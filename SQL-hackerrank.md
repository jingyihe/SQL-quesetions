SQL Hackerrank Questisons:
* Weather Observation Station 5
* Weather Observation Station 6
* Weather Observation Station 7
* Higher Than 75 Marks
* Type of Triangle
* Draw The Triangle 1
* Draw The Triangle 2
* Top Earners
* The Blunder



## Weather Observation Station 5

Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.

Input Format

The STATION table is described as follows:

Field | Type
------------ | -------------
ID | NUMBER
CITY | VARCHAR2(21)
STATE | VARCHAR2(2)
LAT_N | NUMBER
LONG_W | NUMBER

where LAT_N is the northern latitude and LONG_W is the western longitude.

*Sample Input*

Let's say that CITY only has four entries: DEF, ABC, PQRS and WXY

*Sample Output*

ABC 3
PQRS 4

*Explanation*

When ordered alphabetically, the CITY names are listed as ABC, DEF, PQRS, and WXY, with the respective lengths  and . The longest-named city is obviously PQRS, but there are  options for shortest-named city; we choose ABC, because it comes first alphabetically.

Note
You can write two separate queries to get the desired output. It need not be a single query.

**Solution**
```sql
select min(t.city), t.len
from (
        select city, len(city) len,
               max(len(city)) over() maxlen,
               min(len(city)) over() minlen
          from station
       ) t
 where t.len in(t.minlen,t.maxlen)
 group by t.len
```

## Weather Observation Station 6

Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.

Input Format

The **STATION** table is described as follows:

Field | Type
------------ | -------------
ID | NUMBER
CITY | VARCHAR2(21)
STATE | VARCHAR2(2)
LAT_N | NUMBER
LONG_W | NUMBER


where LAT_N is the northern latitude and LONG_W is the western longitude.


**Solution**

```sql
SELECT DISTINCT CITY FROM STATION
WHERE lower(substring(CITY, 1,1)) in ('a', 'e','i','o','u');
```

## Weather Observation Station 7

Query the list of *CITY* names ending with vowels (a, e, i, o, u) from **STATION**. Your result *cannot* contain duplicates.

**Input Format**

The **STATION** table is described as follows: 



| Field  | Type         |
| ------ | ------------ |
| ID     | NUMBER       |
| CITY   | VARCHAR2(21) |
| STATE  | VARCHAR2(2)  |
| LAT_N  | NUMBER       |
| LONG_W | NUMBER       |

where LAT_N is the northern latitude and LONG_W is the western longitude.
**Solution**

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE lower(right(CITY,  1)) in ('a','e','i','o','u');
```

## Higher Than 75 Marks

Query the Name of any student in STUDENTS who scored higher than 75 Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.

Input Format

The STUDENTS table is described as follows:

| Column | Type    |
| ------ | ------- |
| ID     | INTEGER |
| NAME   | STRING  |
| MARKS  | INTEGER |

The Name column only contains uppercase (A-Z) and lowercase (a-z) letters.

Sample Input

| ID   | NAME     | MARKS |
| ---- | -------- | ----- |
| 1    | ASHLEY   | 81    |
| 2    | SAMANTHA | 75    |
| 4    | JULIA    | 76    |
| 3    | JULIA    | 84    |

*Sample Output*

Ashley 

Julia 

Belvet

Explanation

Only Ashley, Julia, and Belvet have Marks > 75. If you look at the last three characters of each of their names, there are no duplicates and 'ley' < 'lia' < 'vet'.

**Solution**

```sql
SELECT NAME FROM STUDENTS WHERE MARKS > 75 ORDER BY RIGHT(NAME, 3), ID;    
```



## Type of Triangle

Write a query identifying the type of each record in the **TRIANGLES** table using its three side lengths. Output one of the following statements for each record in the table:

- **Equilateral**: It’s a triangle with 3 sides of equal length.
- **Isosceles**: It’s a triangle with 2 sides of equal length.
- **Scalene**: It’s a triangle with 3 sides of differing lengths.
- **Not a Triangle**: The given values of A, B, and C don’t form a triangle.

**Input Format**
The **TRIANGLES** table is described as follows:

| Column | Type    |
| :----- | :------ |
| A      | Integer |
| B      | Integer |
| C      | Integer |

Each row in the table denotes the lengths of each of a triangle’s three sides.

**Sample Input**

| A    | B    | C    |
| :--- | :--- | :--- |
| 20   | 20   | 23   |
| 20   | 20   | 20   |
| 20   | 21   | 22   |
| 13   | 14   | 30   |

**Sample Output**

> Isosceles
> Equilateral
> Scalene
> Not A Triangle

**Explanation**
Values in the tuple (20,20,23) form an Isosceles triangle, because A=B.
Values in the tuple (20,20,20) form an Equilateral triangle, because A=B=C.
Values in the tuple (20,21,22) form a Scalene triangle, because A≠B≠C.
Values in the tuple (13,14,30) cannot form a triangle because the combined value of sides A and B is not larger than that of side C.



**Solution**

```sql
SELECT 
    case when A+B <= C or B+C <= A or A+C <= B then 'Not A Triangle'
        when A=B and A=C and B=C then 'Equilateral'
        when A!=B and A!=C and B!=C then 'Scalene'
        else 'Isosceles' end as count
From TRIANGLES;
```





## Draw The Triangle 1

*P(R)* represents a pattern drawn by Julia in *R* rows. The following pattern represents *P(5)*:

 \* \* \* \* \*
 \* \* \* \*
 \* \* \*
 * *
 *

Write a query to print the pattern *P(20)*.

**Solution**

```sql
DECLARE @var int              
SELECT @var = 20              
WHILE @var > 0                
BEGIN                         
PRINT replicate('* ', @var)   
SET @var = @var - 1           
END ;
```







## Draw The Triangle 2

*P(R)* represents a pattern drawn by Julia in *R* rows. The following pattern represents *P(5)*:

*
* * 
* * * 
* * * *
* * * * *


Write a query to print the pattern *P(20)*.

**Solution**

```sql
DeCLARE @var int
SELECT @var = 1
while @var < 21
BEGIN
PRINT replicate('* ', @var)
SET @var = @var + 1
END;
```

More patterns : https://www.geeksforgeeks.org/print-different-star-patterns-sql/





## Top Earners

We define an employee’s *total earnings* to be their monthly *salary x months* worked, and the *maximum total earnings* to be the maximum total earnings for any employee in the **Employee** table. Write a query to find the *maximum total earnings* for all employees as well as the total number of employees who have maximum total earnings. Then print these values as space-separated integers.

**Input Format**
The **Employee** table containing employee data for a company is described as follows:

|   Column    |  Type   |
| :---------: | :-----: |
| employee_id | Integer |
|    name     | String  |
|   months    | Integer |
|   salary    | Integer |

where *employee_id* is an employee’s ID number, *name* is their name, *months* is the total number of months they’ve been working for the company, and *salary* is the their monthly salary.

**Sample Input**

| employee_id |   name   | months | salary |
| :---------: | :------: | :----: | :----: |
|    12228    |   Rose   |   15   |  1968  |
|    33645    |  Angela  |   1    |  3443  |
|    45692    |  Frank   |   17   |  1608  |
|    56118    | Patrick  |   7    |  1345  |
|    59725    |   Lisa   |   11   |  2330  |
|    74197    | Kimberly |   16   |  4372  |
|    78454    |  Bonnie  |   8    |  1771  |
|    83565    | Michael  |   6    |  2017  |
|    98607    |   Todd   |   5    |  3396  |
|    99989    |   Joe    |   9    |  3573  |

**Sample Output**

> 69952 1

**Explanation**
The table and earnings data is depicted in the following diagram:

| employee_id |   name   | months | salary | earnings |
| :---------: | :------: | :----: | :----: | :------: |
|    12228    |   Rose   |   15   |  1968  |  29520   |
|    33645    |  Angela  |   1    |  3443  |   3443   |
|    45692    |  Frank   |   17   |  1608  |  27336   |
|    56118    | Patrick  |   7    |  1345  |   9415   |
|    59725    |   Lisa   |   11   |  2330  |  25630   |
|    74197    | Kimberly |   16   |  4372  |  69952   |
|    78454    |  Bonnie  |   8    |  1771  |  14168   |
|    83565    | Michael  |   6    |  2017  |  12102   |
|    98607    |   Todd   |   5    |  3396  |  16980   |
|    99989    |   Joe    |   9    |  3573  |  32157   |

The maximum *earnings* value is 69952. The only employee with *earnings* = 69952 is *Kimberly*, so we print the maximum *earnings* value (69952) and a count of the number of employees who have earned $69952 (which is 1) as two space-separated values.



**Solution**

```sql
SELECT (months*salary) as earning, count(employee_id)
FROM EMPLOYEE
GROUP BY earning
ORDER by EARning DESC LIMIT 1;
```







## The Blunder

Samantha was tasked with calculating the average monthly salaries for all employees in the **EMPLOYEES** table, but did not realize her keyboard’s 0 key was broken until after completing the calculation. She wants your help finding the difference between her miscalculation (using salaries with any zeroes removed), and the actual average salary.

Write a query calculating the amount of error (i.e.: *actual - miscalculated* average monthly salaries), and round it up to the next integer.

**Input Format**
The **EMPLOYEES** table is described as follows:

| Column | Type    |
| :----- | :------ |
| ID     | Integer |
| NAME   | String  |
| Salary | Integer |

**Note**: Salary is measured in dollars per month and its value is < 105.

**Sample Input**

| ID   | Name     | Salary |
| :--- | :------- | :----- |
| 1    | Kristeen | 1420   |
| 2    | Ashley   | 2006   |
| 3    | Julia    | 2210   |
| 4    | Maria    | 3000   |

**Sample Output**

> 2061

**Explanation**
The table below shows the salaries without zeroes as they were entered by Samantha:

| ID   | Name     | Salary |
| :--- | :------- | :----- |
| 1    | Kristeen | 142    |
| 2    | Ashley   | 26     |
| 3    | Julia    | 221    |
| 4    | Maria    | 3      |

Samantha computes an average salary of 98.00. The *actual* average salary is 2159.00.
The resulting error between the two calculations is 2159.00 - 98.00 = 2061.00 which, when rounded to the next integer, is 2061.

**Solution**

```sql
SELECT CEIL(AVG(salary) - AVG(replace(salary, '0', ''))) 
FROM EMPLOYEES;
```


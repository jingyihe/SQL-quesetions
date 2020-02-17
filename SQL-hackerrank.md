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


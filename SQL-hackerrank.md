# Weather Observation Station 5

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




# Weather Observation Station 6
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

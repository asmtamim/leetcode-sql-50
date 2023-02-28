
**1. Query all columns (attributes) for every row in the CITY table.**

```sql
Select * from CITY;
```

**2. Query all columns for a city in CITY with the ID 1661.**

```sql
Select * from CITY Where ID = 1661;
```

**3. Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.**

```sql
Select * from CITY Where COUNTRYCODE = 'JPN';
```

**4. Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN.**

```sql
Select NAME from CITY Where COUNTRYCODE = 'JPN';
```

**5. Query all columns for all American cities in the CITY table with populations larger than 100000. The CountryCode for America is USA.**

```sql
Select * from CITY Where CountryCode = 'USA' AND Population > 100000;
```

**6. Query the NAME field for all American cities in the CITY table with populations larger than 120000. The CountryCode for America is USA.**

```sql
Select NAME from CITY Where CountryCode = 'USA' AND Population > 120000;
```

**7. Query a list of CITY and STATE from the STATION table.**

```sql
Select CITY, STATE from STATION;
```

**8. Query a list of CITY names from STATION for cities that have an even ID number. Print the results in any order, but exclude duplicates from the answer.**

```sql
SELECT distinct CITY from STATION where (ID % 2) = 0 order by CITY ASC;
```

**9. Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.**

```sql
SELECT COUNT(CITY) - COUNT(DISTINCT CITY) FROM STATION;
```

**10. Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.**

```sql
Select DISTINCT(CITY) from STATION 
where CITY LIKE 'A%' OR CITY LIKE 'E%' OR CITY LIKE 'I%' OR CITY LIKE 'O%' OR CITY LIKE 'U%' 
Order by CITY ASC;
```

**11. Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.**

```sql
SELECT COUNT(CITY) - COUNT(DISTINCT CITY) FROM STATION;
```

**12. Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.**

```sql
SELECT COUNT(CITY) - COUNT(DISTINCT CITY) FROM STATION;
```

**13. Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.**

```sql
SELECT COUNT(CITY) - COUNT(DISTINCT CITY) FROM STATION;
```

**14. Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.**

```sql
SELECT COUNT(CITY) - COUNT(DISTINCT CITY) FROM STATION;
```

**15. Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.**

```sql
SELECT COUNT(CITY) - COUNT(DISTINCT CITY) FROM STATION;
```

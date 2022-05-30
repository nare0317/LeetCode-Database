# Placements - Find 

## Description

You are given three tables: Students, Friends and Packages. Students contains two columns: ID and Name. Friends contains two columns: ID and Friend_ID (ID of the ONLY best friend). Packages contains two columns: ID and Salary (offered salary in $ thousands per month).

Table: Students

```
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| ID           | int     |
| Name         | varchar |
+--------------+---------+
``` 

Table: Friends

```
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| ID           | int     |
| Friend_id    | int     |
+--------------+---------+
``` 
Table: Packages

```
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| ID           | int     |
| Salary       | int     |
+--------------+---------+
``` 

Write a query to output the names of those students whose best friends got offered a higher salary than them. Names must be ordered by the salary amount offered to the best friends. It is guaranteed that no two students got same salary offer.


## Explanation

See the following table:

![image](https://user-images.githubusercontent.com/40656125/171009715-1db9bef2-1b3c-4153-bf43-82f39ca0449e.png)


Now,

Samantha's best friend got offered a higher salary than her at 11.55
Julia's best friend got offered a higher salary than her at 12.12
Scarlet's best friend got offered a higher salary than her at 15.2
Ashley's best friend did NOT get offered a higher salary than her
The name output, when ordered by the salary offered to their friends, will be:
- Samantha
- Julia
- Scarlet


## My Answer 

```SQL
-- MS SQL Server 
WITH RESULT(ID, NAME, FRIEND_ID, MY_SALARY, FRIEND_SALARY)
AS
(
SELECT A.ID, A.Name, B.Friend_ID, C.Salary AS MY_SALARY, D.Salary AS FRIEND_SALARY
FROM Students AS A 
JOIN Friends AS B ON A.ID = B.ID
JOIN Packages AS C ON A.ID = C.ID
JOIN Packages AS D ON B.Friend_ID = D.ID    
)
SELECT NAME 
FROM RESULT
WHERE MY_SALARY < FRIEND_SALARY
ORDER BY FRIEND_SALARY
```

## Other Solutions 

```SQL
-- Oracle 
SELECT name
FROM
(
SELECT DISTINCT s.name , fo.salary
FROM Students s, Packages so, Friends f, Packages fo
WHERE s.id = so.id
AND f.friend_id = fo.id
AND s.id = f.id
AND fo.salary > so.salary
ORDER BY fo.salary);
```

```SQL
-- Mysql
select s.name from students s
inner join friends f on f.id = s.id
inner join packages p on p.id = s.id
where p.salary < (select pp.salary from packages pp where pp.id = f.friend_id)
order by (select pp.salary from packages pp where pp.id = f.friend_id) asc;
```

## References
1. Problem: [HackerRank - SQL>Advanced Join>Placements](https://www.hackerrank.com/challenges/placements/problem?isFullScreen=true)
2. CTE Expression: [MS SQL - CTE Expression](https://docs.microsoft.com/en-us/sql/t-sql/queries/with-common-table-expression-transact-sql?view=sql-server-ver16)



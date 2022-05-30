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

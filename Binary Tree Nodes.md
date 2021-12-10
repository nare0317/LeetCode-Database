# Binary Tree Nodes

## Description


You are given a table, BST, containing two columns: N and P, where N represents the value of a node in Binary Tree, and P is the parent of N.
![image](https://user-images.githubusercontent.com/40656125/145591987-cf45c1ec-33b9-4ecf-bbe1-aa0ddda68041.png)


Write a query to find the node type of Binary Tree ordered by the value of the node. Output one of the following for each node:

- Root: If node is root node.
- Leaf: If node is leaf node.
- Inner: If node is neither root nor leaf node.

### Sample Input

![image](https://user-images.githubusercontent.com/40656125/145592037-c1f1d668-5d78-4c41-81c9-9b2bfa4faf31.png)


### Sample Output

```
1 Leaf
2 Inner
3 Leaf
5 Root
6 Leaf
8 Inner
9 Leaf
```

### Explanation

The Binary Tree below illustrates the sample:

![image](https://user-images.githubusercontent.com/40656125/145592092-ef177fa4-de44-4c02-88ac-2a234ec5df3c.png)


## My Answer 

```SQL
-- MS SQL Server 
SELECT A.N, CASE WHEN A.P IS NULL THEN "Root"
                 WHEN B.P IS NULL THEN "Leaf"
                 ELSE "Inner" END 
  FROM BST AS A
  LEFT OUTER JOIN (SELECT DISTINCT P 
                     FROM BST          ) AS B ON A.N = B.P
 ORDER BY A.N
```

## Other Solutions 


```SQL
-- MySQL 
SELECT CASE
	WHEN P IS NULL THEN CONCAT(N, ' Root')
	WHEN N IN (SELECT DISTINCT P FROM BST) THEN CONCAT(N, ' Inner')
	ELSE CONCAT(N, ' Leaf')
	END
FROM BST
ORDER BY N ASC
```

```SQL
-- MySQL
SELECT N,
    CASE
        WHEN P IS null THEN 'Root'
        WHEN N IN (SELECT DISTINCT P FROM BST) THEN  'Inner'
        ELSE 'Leaf'
    END
FROM BST ORDER BY N;
```
```SQL
-- MS SQL Server 
SELECT
    N,
    CASE
        WHEN P IS NULL THEN 'Root'
        WHEN N NOT IN ( SELECT P FROM BST ) THEN 'Leaf'
        ELSE 'Inner'
    END
FROM BST
ORDER BY N ASC
```


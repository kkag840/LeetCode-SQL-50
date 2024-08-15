# ORACLE 

# The Number of Employees Which Report to Each Employee
[LeetCode Problem Description](https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT m.employee_id,m.name,COUNT(e.reports_to) reports_count,ROUND(AVG(e.age)) average_age
FROM employees m,employees e
WHERE m.employee_id=e.reports_to
GROUP BY m.employee_id,e.reports_to,m.name
ORDER BY m.employee_id;
```

# Primary Department for Each Employee
[LeetCode Problem Description](https://leetcode.com/problems/primary-department-for-each-employee/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT employee_id,department_id FROM Employee WHERE primary_flag='Y'
UNION
SELECT employee_id,department_id
FROM employee
WHERE  employee_id IN(SELECT employee_id
                      FROM Employee
                      GROUP BY employee_id
                      HAVING COUNT(*)=1
                      );
```

# Triangle Judgement
[LeetCode Problem Description](https://leetcode.com/problems/triangle-judgement/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT x,y,z, CASE
                  WHEN(x+y>z AND x+z>y AND y+z>x)
                  THEN
                        'Yes'
                  else
                        'No'
                  end AS triangle 
FROM Triangle;
```

# Consecutive Numbers
[LeetCode Problem Description](https://leetcode.com/problems/consecutive-numbers/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT DISTINCT i.num ConsecutiveNums
FROM Logs i
WHERE i.num=(SELECT num FROM Logs 
                WHERE i.id+1=id) AND 
      i.num=(SELECT num FROM Logs
                WHERE i.id+2=id);
```

# Product Price at a Given Date
[LeetCode Problem Description](https://leetcode.com/problems/product-price-at-a-given-date/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT product_id,new_price price
FROM Products
WHERE (product_id,change_date) IN(SELECT product_id,MAX(change_date)
                                   FROM Products
                                   WHERE change_date<='2019-08-16'
                                   GROUP BY product_id)
UNION
SELECT product_id,10
FROM Products
WHERE (product_id,change_date) IN(SELECT product_id,MIN(change_date)
                                   FROM Products
                                   WHERE change_date>'2019-08-16' AND 
                                   product_id NOT IN(SELECT product_id
                                                     FROM Products
                                                      WHERE change_date<='2019-08-16'
                                                      GROUP BY product_id) 
                                   GROUP BY product_id)
```

# Last Person to Fit in the Bus
[LeetCode Problem Description](https://leetcode.com/problems/last-person-to-fit-in-the-bus/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT person_name
FROM (
        (SELECT turn,person_name
         FROM (SELECT *
               FROM Queue
               ORDER BY turn) ls
         WHERE 1000>=(SELECT sum(weight) weight
                      FROM queue WHERE
                      turn<=ls.turn)
          )
      ORDER BY turn DESC
    )
WHERE ROWNUM=1;
```

# Count Salary Categories
[LeetCode Problem Description](https://leetcode.com/problems/count-salary-categories/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT 'Low Salary' category, SUM(CASE WHEN(income<20000)
                                            THEN 1
                                            ELSE 0
                                            END
                                  ) accounts_count FROM Accounts
UNION ALL
SELECT 'Average Salary' category, NVL(SUM(CASE WHEN(income>=20000 AND income<=50000)
                                                    THEN 1
                                                    ELSE 0
                                                    END
                                          ),0) accounts_count FROM Accounts
UNION ALL
SELECT 'High Salary' category, SUM(CASE WHEN(income>50000)
                                              THEN 1
                                              ELSE 0
                                              END
                                  ) accounts_count FROM Accounts
```

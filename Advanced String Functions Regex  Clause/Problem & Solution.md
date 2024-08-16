# ORACLE 

# Fix Names in a Table
[LeetCode Problem Description](https://leetcode.com/problems/fix-names-in-a-table/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT user_id, UPPER(SUBSTR(NAME,1,1))||LOWER(SUBSTR(NAME,2)) as name
FROM Users
order by user_id;
```

# Patients With a Condition
[LeetCode Problem Description](https://leetcode.com/problems/patients-with-a-condition/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT* FROM Patients
 WHERE conditions LIKE 'DIAB1%' OR conditions LIKE '% DIAB1%';
```

# Delete Duplicate Emails
[LeetCode Problem Description](https://leetcode.com/problems/delete-duplicate-emails/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
DELETE FROM person
WHERE id NOT IN(SELECT MIN(id) FROM Person GROUP BY email);
```

# Second Highest Salary
[LeetCode Problem Description](https://leetcode.com/problems/second-highest-salary/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT MAX(salary) SecondHighestSalary FROM Employee 
WHERE SALARY IN(SELECT SALARY
                FROM EMPLOYEE
                WHERE SALARY!=(SELECT MAX(SALARY)
                                FROM EMPLOYEE));
```

# Group Sold Products By The Date
[LeetCode Problem Description](https://leetcode.com/problems/group-sold-products-by-the-date/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT TO_CHAR(sell_date,'YYYY-MM-DD') sell_date,COUNT(DISTINCT product) num_sold,LISTAGG(product,',') WITHIN GROUP(ORDER BY product) products
FROM (SELECT DISTINCT product,sell_date FROM activities)
GROUP BY sell_date;
ORDER BY sell_date;
```

# List the Products Ordered in a Period
[LeetCode Problem Description](https://leetcode.com/problems/list-the-products-ordered-in-a-period/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT product_name,unit
FROM products p,(SELECT product_id,SUM(unit) unit 
                FROM Orders 
                WHERE TO_CHAR(order_date,'yyyy-mm')='2020-02'
                GROUP BY product_id) u
WHERE p.product_id=u.product_id AND unit>=100;
```

# Find Users With Valid E-Mails
[LeetCode Problem Description](https://leetcode.com/problems/find-users-with-valid-e-mails/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT *
FROM Users
WHERE REGEXP_LIKE(mail,'^[a-zA-Z][a-zA-Z0-9_.-]*@leetcode[.]com$');
```

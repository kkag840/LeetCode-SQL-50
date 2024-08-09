# ORACLE 

# Replace Employee ID With The Unique Identifier
[LeetCode Problem Description](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT unique_id,name
FROM Employees e,EmployeeUNI i
WHERE e.id=i.id(+);
```

#  Product Sales Analysis I
[LeetCode Problem Description](https://leetcode.com/problems/product-sales-analysis-i/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT product_name,year,price 
FROM sales s,product p
WHERE s.product_id=p.product_id;
```

#  Customer Who Visited but Did Not Make Any Transactions
[LeetCode Problem Description](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/submissions/1175244949/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT customer_id,COUNT(*) count_no_trans 
FROM visits 
where visit_id NOT IN(SELECT visit_id FROM Transactions)
GROUP BY customer_id;
```

#  Rising Temperature
[LeetCode Problem Description](https://leetcode.com/problems/rising-temperature/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT h.ID 
FROM weather h,weather m
WHERE h.recorddate-m.recorddate=1 and h.temperature>m.temperature;
```

#  Average Time of Process per Machine
[LeetCode Problem Description](https://leetcode.com/problems/average-time-of-process-per-machine/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT l.machine_id,ROUND((l.en-f.st)/l.div,3) processing_time
FROM (SELECT machine_id,SUM(timestamp) en,COUNT(*) div FROM Activity
      WHERE activity_type='end' GROUP BY machine_id) l,
      (SELECT machine_id,SUM(timestamp) st FROM Activity
      WHERE activity_type='start' GROUP BY machine_id) f
WHERE l.machine_id=f.machine_id;
```

#  Employee Bonus
[LeetCode Problem Description](https://leetcode.com/problems/employee-bonus/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT name,bonus
FROM employee e,bonus b
WHERE e.empid=b.empid(+) and e.empid
NOT IN(SELECT e.empid 
FROM employee e,bonus b
WHERE bonus>=1000 AND e.empid=b.empid);
```

#  Students and Examinations
[LeetCode Problem Description](https://leetcode.com/problems/students-and-examinations/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT s.student_id,s.student_name,s.subject_name,NVL(COUNT(e.subject_name),0) attended_exams
FROM (SELECT student_id,student_name,subject_name FROM students,subjects) s LEFT OUTER JOIN Examinations e
      ON(s.student_id=e.student_id AND s.subject_name=e.subject_name) 
GROUP BY s.student_id,s.student_name,s.subject_name
ORDER BY student_id,subject_name;
```

#  Managers with at Least 5 Direct Reports
[LeetCode Problem Description](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT name
FROM Employee
WHERE id in(SELECT managerid
            FROM employee
            GROUP BY managerid
            HAVING COUNT(*)>=5);
```

#  Confirmation Rate
[LeetCode Problem Description](https://leetcode.com/problems/confirmation-rate/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT s.user_id,ROUND(NVL(rate,0.0),2) confirmation_rate
FROM signups s,(SELECT user_id,sum(case when(action='confirmed') then 1 else 0 end)/count(*) rate
FROM confirmations
GROUP BY user_id
) c
WHERE s.user_id=c.user_id(+);
```

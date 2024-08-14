# ORACLE 

# Number of Unique Subjects Taught by Each Teacher
[LeetCode Problem Description](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT TEACHER_ID,COUNT(DISTINCT SUBJECT_ID) CNT
FROM TEACHER
GROUP BY TEACHER_ID;
```

# User Activity for the Past 30 Days I
[LeetCode Problem Description](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT TO_CHAR(activity_date,'YYYY-MM-DD') day, COUNT(DISTINCT user_id) active_users
FROM Activity
WHERE activity_date BETWEEN '2019-06-28' AND '2019-07-27'
GROUP BY activity_date;
```

# Product Sales Analysis III
[LeetCode Problem Description](https://leetcode.com/problems/product-sales-analysis-iii/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT product_id,year first_year,quantity,price
FROM Sales
WHERE (year,product_id) IN( SELECT MIN(year),product_id
                                FROM sales
                                GROUP BY product_id);
```

# Classes More Than 5 Students
[LeetCode Problem Description](https://leetcode.com/problems/classes-more-than-5-students/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT CLASS FROM COURSES GROUP BY CLASS HAVING COUNT(CLASS)>=5;
```

# Find Followers Count
[LeetCode Problem Description](https://leetcode.com/problems/find-followers-count/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT USER_ID,COUNT(FOLLOWER_ID) FOLLOWERS_COUNT
FROM FOLLOWERS
GROUP BY USER_ID
ORDER BY USER_ID;
```

# Biggest Single Number
[LeetCode Problem Description](https://leetcode.com/problems/biggest-single-number/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT MAX(NUM) NUM
FROM (SELECT *
      FROM MYNUMBERS
      GROUP BY NUM
      HAVING COUNT(*)=1
      ); 
```

# Customers Who Bought All Products
[LeetCode Problem Description](https://leetcode.com/problems/customers-who-bought-all-products/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT customer_id
FROM Customer
GROUP BY customer_id
HAVING COUNT(DISTINCT product_key)=( SELECT COUNT(*)
                                     FROM Product); 
```

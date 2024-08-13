# ORACLE 

# Not Boring Movies
[LeetCode Problem Description](https://leetcode.com/problems/not-boring-movies/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT *
FROM Cinema
WHERE MOD(ID,2)=1 AND LOWER(description)!='boring' order by rating
```

# Average Selling Price
[LeetCode Problem Description](https://leetcode.com/problems/average-selling-price/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT p.product_id,NVL(ROUND(sum(price*units)/sum(units),2),0.0) average_price
FROM prices p,unitssold u
WHERE p.product_id=u.product_id(+) AND (purchase_date BETWEEN start_date AND end_date OR purchase_date IS NULL)
GROUP BY p.product_id,u.product_id;
```

# Project Employees I
[LeetCode Problem Description](https://leetcode.com/problems/project-employees-i/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT project_id,ROUND(AVG(experience_years),2) average_years
FROM Project p,employee e
WHERE p.employee_id=e.employee_id
GROUP BY project_id;
```

# Percentage of Users Attended a Contest
[LeetCode Problem Description](https://leetcode.com/problems/percentage-of-users-attended-a-contest/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT contest_id,ROUND(COUNT(distinct user_id)/(SELECT COUNT(*) FROM Users)*100,2) percentage
FROM Register
GROUP BY contest_id
ORDER BY percentage desc ,contest_id;
```

# Queries Quality and Percentage
[LeetCode Problem Description](https://leetcode.com/problems/queries-quality-and-percentage/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT query_name,ROUND(SUM(rating/position)/count(*),2) quality,ROUND(SUM(CASE WHEN(rating<3) THEN 1 ELSE 0 END)/count(*)*100,2) poor_query_percentage
FROM Queries
WHERE query_name IS NOT NULL
GROUP BY query_name;
```

# Monthly Transactions I
[LeetCode Problem Description](https://leetcode.com/problems/monthly-transactions-i/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT TO_CHAR(trans_date,'yyyy-mm') month,country,count(*) trans_count,SUM(CASE WHEN(state='approved') THEN 1 ELSE 0 END) approved_count,sum(amount) trans_total_amount,SUM(CASE WHEN(state='approved') THEN amount ELSE 0 END) approved_total_amount 
FROM Transactions
GROUP BY TO_CHAR(trans_date,'yyyy-mm'),country;
```

# Immediate Food Delivery II
[LeetCode Problem Description](https://leetcode.com/problems/immediate-food-delivery-ii/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT ROUND(SUM(CASE WHEN(order_date=customer_pref_delivery_date) THEN 1 ELSE 0 END)/COUNT(DISTINCT customer_id)*100,2) immediate_percentage
FROM Delivery 
WHERE (customer_id,order_date) IN(SELECT customer_id,MIN(order_date) FROM delivery GROUP BY customer_id);
```

# Game Play Analysis IV
[LeetCode Problem Description](https://leetcode.com/problems/game-play-analysis-iv/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT ROUND(count(b.player_id)/COUNT(a.player_id),2) fraction
FROM activity a LEFT OUTER JOIN activity b
ON b.event_date-a.event_date=1 AND a.player_id=b.player_id
WHERE (a.player_id,a.event_date) IN(SELECT player_id,MIN(event_date)
                                    FROM activity
                                    GROUP BY player_id
                                    );
```

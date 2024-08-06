# ORACLE 

# Recyclable and Low Fat Products
[LeetCode Problem Description](https://leetcode.com/problems/recyclable-and-low-fat-products/description/?envType=study-plan-v2&envId=top-sql-50)
## Solution
```sql
SELECT product_id 
FROM Products 
WHERE low_fats = 'Y' AND recyclable = 'Y';
```

# Find Customer Referee
[LeetCode Problem Description](https://leetcode.com/problems/find-customer-referee/description/?envType=study-plan-v2&envId=top-sql-50)
## Solution
```sql
SELECT name
FROM Customer
WHERE referee_id!=2 OR referee_id IS NULL;
```

# Big Countries
[LeetCode Problem Description](https://leetcode.com/problems/big-countries/description/?envType=study-plan-v2&envId=top-sql-50)
## Solution
```sql
SELECT name,population,area
FROM World
WHERE area>= 3000000 or population>= 25000000;
```

# Article Views I
[LeetCode Problem Description](https://leetcode.com/problems/article-views-i/description/?envType=study-plan-v2&envId=top-sql-50)
## Solution
```sql
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id=viewer_id ORDER BY author_id;
```

# Invalid Tweets
[LeetCode Problem Description](https://leetcode.com/problems/invalid-tweets/description/?envType=study-plan-v2&envId=top-sql-50)
## Solution
```sql
SELECT tweet_id
FROM Tweets
WHERE LENGTH(content)>15;
```

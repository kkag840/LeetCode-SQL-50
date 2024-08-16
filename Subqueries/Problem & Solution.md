# ORACLE 

# Employees Whose Manager Left the Company
[LeetCode Problem Description](https://leetcode.com/problems/employees-whose-manager-left-the-company/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT employee_id
FROM employees
WHERE SALARY<30000 AND manager_id NOT IN(SELECT employee_id FROM employees)
order by employee_id;
```

# Exchange Seats
[LeetCode Problem Description](https://leetcode.com/problems/exchange-seats/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT  o.id,e.student 
FROM Seat o,Seat e
WHERE MOD(e.id,2)=1 AND e.id+1=o.id
      OR MOD(e.id,2)=0 AND e.id-1=o.id
      OR MOD(o.id,2)=1 AND e.id=o.id AND o.id=(SELECT COUNT(*) FROM Seat)
ORDER BY o.id;
```

# Movie Rating
[LeetCode Problem Description](https://leetcode.com/problems/movie-rating/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT name results
FROM (SELECT name
      FROM (
            SELECT user_id
             FROM MovieRating
             GROUP BY user_id
              HAVING COUNT(*)=(SELECT MAX(COUNT(*)) FROM MovieRating GROUP BY user_id)
           ) m,Users u
       WHERE m.user_id=u.user_id
       ORDER BY name)
WHERE ROWNUM=1
UNION ALL
SELECT title
FROM( SELECT title
      FROM (
             SELECT movie_id
             FROM MovieRating
             WHERE TO_CHAR(created_at,'yyyy-mm')='2020-02'
             GROUP BY movie_id
             HAVING AVG(rating)=(SELECT MAX(AVG(rating)) FROM MovieRating WHERE TO_CHAR(created_at,'yyyy-mm')='2020-02' GROUP BY movie_id)
           ) r,movies  m
      WHERE m.movie_id=r.movie_id
      ORDER BY title
    )
WHERE ROWNUM=1;
```

# Restaurant Growth
[LeetCode Problem Description](https://leetcode.com/problems/restaurant-growth/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT TO_CHAR(L.visited_on,'YYYY-MM-DD') visited_on, SUM(R.amount) amount, ROUND(SUM(R.amount)/7,2) average_amount
FROM  (
          SELECT visited_on,SUM(amount) amount
          FROM Customer
          GROUP BY visited_on
       ) L,
       (
          SELECT visited_on,SUM(amount) amount
          FROM Customer
          GROUP BY visited_on
       ) R
WHERE L.visited_on-R.visited_on>=0 AND L.visited_on-R.visited_on<=6
GROUP BY L.visited_on
HAVING COUNT(L.visited_on)=7
ORDER BY L.visited_on;
```

# Friend Requests II: Who Has the Most Friends
[LeetCode Problem Description](https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT id,num
FROM (
       SELECT friend id,count(friend) num
       FROM (SELECT requester_id friend FROM RequestAccepted 
             UNION ALL
             SELECT accepter_id friend FROM RequestAccepted
            )
       GROUP BY friend
       ORDER BY num DESC
       )
WHERE ROWNUM=1;
```

# Investments in 2016
[LeetCode Problem Description](https://leetcode.com/problems/investments-in-2016/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT SUM(tiv_2016) tiv_2016
FROM Insurance
WHERE tiv_2015 IN (SELECT tiv_2015
                   FROM Insurance
                   GROUP BY tiv_2015
                   HAVING COUNT(*)>1)
        AND
        (lat,lon) IN(SELECT lat,lon
                    FROM Insurance
                    GROUP BY lat,lon
                    HAVING COUNT(*)=1);
```

# Department Top Three Salaries
[LeetCode Problem Description](https://leetcode.com/problems/department-top-three-salaries/description/?envType=study-plan-v2&envId=top-sql-50);
## Solution
```sql
SELECT d.name department, o.name employee,o.salary
FROM Employee o,Department d
WHERE o.salary IN(SELECT salary 
                FROM (SELECT DISTINCT salary,departmentId
                         FROM employee 
                          ORDER BY salary DESC) i
                WHERE ROWNUM<=3 AND i.departmentId=o.departmentId
                ) AND o.departmentId=d.id;
```

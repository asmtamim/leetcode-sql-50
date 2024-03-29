
**01/ 1757. Recyclable and Low Fat Products.**

```sql
select product_id from Products where low_fats = 'Y' and recyclable = 'Y'
```

**02/ 584. Find Customer Referee.**

```sql
select name from Customer 
    where referee_id <> '2' or referee_id is null
```

**03/ 595. Big Countries.**

```sql
select name, population, area from World
    where population > '24999999' or area > '2999999'
```

**04/ 1148. Article Views I.**

```sql
select DISTINCT author_id as id from Views 
    where author_id = viewer_id
        order by author_id asc
```

**05/ 1683. Invalid Tweets.**

```sql
select tweet_id from Tweets
    where LEN(content) > 15
```

**06/ 1378. Replace Employee ID With The Unique Identifier.**

```sql
select a.unique_id, b.name from EmployeeUNI a 
    right join Employees b on a.id = b.id
```

**07/ 1068. Product Sales Analysis I.**

```sql
select a.product_name, b.year, b.price from Product a
    right join Sales b on a.product_id = b.product_id
```

**08/ 1581. Customer Who Visited but Did Not Make Any Transactions.**

```sql
SELECT customer_id, COUNT(*) as count_no_trans FROM Visits
WHERE visit_id NOT IN (SELECT DISTINCT visit_id FROM Transactions)
GROUP BY customer_id;
```

```sql
SELECT v.customer_id, COUNT(v.visit_id) AS count_no_trans FROM Visits v
LEFT JOIN Transactions t ON v.visit_id = t.visit_id
WHERE t.transaction_id IS NULL
GROUP BY v.customer_id
```

**09/ 197. Rising Temperature.**

```sql
SELECT t.id FROM Weather t
    INNER JOIN Weather y ON DATEDIFF(DAY, y.recordDate, t.recordDate) = 1 
        AND t.temperature > y.temperature
```

```sql
SELECT DISTINCT a.Id FROM Weather a, Weather b
  WHERE a.Temperature > b.Temperature AND DATEDIFF(day, a.Recorddate, b.Recorddate) = 1
```

**10/ 1661. Average Time of Process per Machine.**

```sql
SELECT a.machine_id, ROUND(AVG(b.timestamp - a.timestamp), 3) AS processing_time FROM Activity a
JOIN Activity b ON a.machine_id = b.machine_id AND a.process_id = b.process_id
                                               AND a.activity_type = 'start' AND b.activity_type = 'end' 
    GROUP BY a.machine_id
```

**11/ 577. Employee Bonus.**

```sql
SELECT e.name, b.bonus FROM Employee e 
    LEFT JOIN Bonus b ON e.empId = b.empId
        WHERE b.bonus IS NULL OR b.bonus < 1000
```

**12/ 1280. Students and Examinations.**

```sql
SELECT s.student_id, s.student_name, u.subject_name, COUNT(e.subject_name) AS attended_exams
FROM Students s CROSS JOIN Subjects u  
    LEFT JOIN Examinations e ON s.student_id = e.student_id AND u.subject_name = e.subject_name 
        GROUP BY s.student_id, s.student_name, u.subject_name
        ORDER BY s.student_id, u.subject_name
```

**13/ 570. Managers with at Least 5 Direct Reports.**

```sql
SELECT name FROM Employee
    WHERE id in (SELECT managerId FROM Employee GROUP BY managerId HAVING COUNT(managerId) >= 5)
```

```sql
SELECT e2.name FROM Employee e1 
    JOIN Employee e2 ON e1.managerId = e2.id 
        GROUP BY e1.managerId HAVING count(e1.id) >= 5
```

**14/ 1934. Confirmation Rate.**

```sql
SELECT s.user_id,
    ISNULL(ROUND(AVG(CASE WHEN c.action = 'confirmed' THEN 1.0 ELSE 0.0 END), 2), 0) AS confirmation_rate
FROM Signups s
    LEFT JOIN Confirmations c ON s.user_id = c.user_id
    GROUP BY s.user_id
```

**15/ 620. Not Boring Movies.**

```sql
select * from Cinema where description <> 'boring' and (id % 2) = '1' 
    order by rating desc
```

**16/ 1251. Average Selling Price.**

```sql
SELECT p.product_id,
ISNULL(ROUND(SUM(p.price * u.units) * 1.0 / SUM(u.units), 2), 0) AS average_price FROM Prices p
    LEFT JOIN UnitsSold u ON p.product_id = u.product_id AND (u.purchase_date BETWEEN p.start_date AND p.end_date)
    GROUP BY p.product_id
```

**17/ 1075. Project Employees I.**

```sql
select project_id , round(avg(experience_years), 2) as average_years from Project p
    left join Employee e on p.employee_id = e.employee_id
        group by project_id
```

**18/ 1633. Percentage of Users Attended a Contest.**

```sql
SELECT contest_id, round(count(user_id)*100.00/(select count(*) from users),2) AS percentage FROM Register
    GROUP BY contest_id ORDER BY percentage DESC, contest_id
```

**19/ 1211. Queries Quality and Percentage.**

```sql
SELECT query_name, ROUND(AVG(CAST(rating AS DECIMAL) / position), 2) AS quality,
    ROUND(SUM(CASE WHEN rating < 3 THEN 1.0 ELSE 0.0 END) * 100 / COUNT(*), 2) AS poor_query_percentage
FROM Queries WHERE query_name IS NOT NULL
    GROUP BY query_name
```

**20/ 1193. Monthly Transactions I.**

```sql
SELECT FORMAT(trans_date, 'yyyy-MM') AS month, country,
  COUNT(*) AS trans_count,
  SUM(CASE WHEN state = 'approved' THEN 1 ELSE 0 END) AS approved_count,
  SUM(amount) AS trans_total_amount,
  SUM(CASE WHEN state = 'approved' THEN amount ELSE 0 END) AS approved_total_amount
FROM Transactions
    GROUP BY FORMAT(trans_date, 'yyyy-MM'), country
```

**21/ 1174. Immediate Food Delivery II.**

```sql
SELECT ROUND(AVG(order_date = customer_pref_delivery_date) * 100, 2) AS immediate_percentage FROM Delivery
    WHERE (customer_id, order_date) IN (SELECT customer_id, MIN(order_date) FROM Delivery GROUP BY 1)
```

**22/ 550. Game Play Analysis IV.**

```sql
SELECT ROUND(SUM(case
                    when DATEADD(day,1,A.event_date) = B.event_date THEN 1
                    ELSE 0 END) * 1.00 / COUNT(DISTINCT A.player_id), 2) as fraction
FROM (SELECT player_id, min(event_date) as event_date from activity group by player_id) as A 
    join activity as B on A.player_id = B.player_id
```

**23/ 2356. Number of Unique Subjects Taught by Each Teacher.**

```sql
SELECT teacher_id, COUNT(DISTINCT subject_id) AS cnt FROM Teacher
    GROUP BY teacher_id
```

**24/ 1141. User Activity for the Past 30 Days I.**

```sql
SELECT activity_date AS day, COUNT(DISTINCT user_id) AS active_users FROM Activity
    WHERE activity_date BETWEEN '2019-06-28' AND '2019-07-27'
        GROUP BY activity_date;
```

**25/ 1070. Product Sales Analysis III.**

```sql
SELECT product_id, year AS first_year, quantity, price FROM Sales
    WHERE (product_id, year) IN (SELECT product_id, MIN(year) AS year FROM Sales GROUP BY product_id);
```

**26/ 596. Classes More Than 5 Students.**

```sql
SELECT class FROM Courses 
    GROUP BY class 
        HAVING COUNT(DISTINCT student) >= 5
```

**27/ 1729. Find Followers Count.**

```sql
SELECT user_id, count(DISTINCT follower_id) AS followers_count FROM Followers 
    GROUP BY user_id
```

**28/ 619. Biggest Single Number.**

```sql
SELECT MAX(T.num) AS num FROM (SELECT COUNT(num) AS counts, num FROM MyNumbers GROUP BY num) AS T
    WHERE T.counts = 1
```

**29/ 1045. Customers Who Bought All Products.**

```sql
SELECT customer_id FROM Customer
    GROUP BY customer_id
    HAVING COUNT(DISTINCT product_key) = (SELECT COUNT(*) FROM Product)
```

**30/ 1731. The Number of Employees Which Report to Each Employee.**

```sql
SELECT e2.employee_id, e2.name, COUNT(e1.reports_to) AS reports_count,
    ROUND(AVG(CONVERT(FLOAT, e1.age)), 0) AS average_age FROM Employees e1 
        JOIN Employees e2 ON e1.reports_to = e2.employee_id
            GROUP BY e2.employee_id, e2.name
            ORDER BY e2.employee_id
```

**31/ 1789. Primary Department for Each Employee.**

```sql
SELECT employee_id, department_id FROM employee
    GROUP BY employee_id
    HAVING COUNT(employee_id) = 1

UNION

SELECT employee_id, department_id FROM employee
    WHERE primary_flag = 'Y'
```

**32/ 610. Triangle Judgement.**

```sql
SELECT x, y, z, (CASE
                    WHEN x + y > z AND x + z > y AND y + z > x THEN 'Yes'
                    ELSE 'No' END) AS 'triangle'
FROM Triangle
```

**33/ 22. Your result cannot contain duplicates.**

```sql

```

**34/ 20. Your result cannot contain duplicates.**

```sql

```

**35/ 21. Your result cannot contain duplicates.**

```sql

```

**36/ 22. Your result cannot contain duplicates.**

```sql

```

**37/ 1978. Employees Whose Manager Left the Company.**

```sql
SELECT e1.employee_id FROM Employees e1
WHERE e1.salary < 30000 AND e1.manager_id IS NOT NULL
    AND NOT EXISTS (SELECT 1 FROM Employees e2 WHERE e2.employee_id = e1.manager_id)
        ORDER BY e1.employee_id
```

**38/ 21. Your result cannot contain duplicates.**

```sql

```

**39/ 22. Your result cannot contain duplicates.**

```sql

```

**40/ 22. Your result cannot contain duplicates.**

```sql

```

**41/ 20. Your result cannot contain duplicates.**

```sql

```

**42/ 21. Your result cannot contain duplicates.**

```sql

```

**43/ 22. Your result cannot contain duplicates.**

```sql

```

**44/ 20. Your result cannot contain duplicates.**

```sql

```

**45/ 21. Your result cannot contain duplicates.**

```sql

```

**46/ 22. Your result cannot contain duplicates.**

```sql

```

**47/ 22. Your result cannot contain duplicates.**

```sql

```

**48/ 20. Your result cannot contain duplicates.**

```sql

```

**49/ 21. Your result cannot contain duplicates.**

```sql

```

**50/ 22. Your result cannot contain duplicates.**

```sql

```

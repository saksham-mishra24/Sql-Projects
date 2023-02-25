# 🍜 Case #1: Consumers Table 

## Solution

View the complete syntax [here](https://github.com/katiehuangx/8-Week-SQL-Challenge/blob/main/Case%20Study%20%231%20-%20Danny's%20Diner/SQL%20Syntax/Danny's%20Diner.sql).

***

###  These SQL queries analyzes the customers & their cuisines preferences. This helps to understand the types of customers & their preferences.

### 1. Total Customers in each state ?


```sql
SELECT 
   State, count(consumer_id) as Total_Customers
FROM consumers
GROUP BY State
Order BY Total_Customers DESC
```

<details>
<summary>
Click here for Solution!
</summary>

  ![image](https://user-images.githubusercontent.com/120908587/221339056-bc051c8c-7801-4697-a41a-e8e22f0b02ee.png)

</details>

### 2. Total Customers in each city ?

```sql
SELECT 
	 city,
	 count(consumer_id) as Total_Customers
FROM 	 consumers
GROUP BY city
Order BY Total_Customers DESC	
```

<details>
<summary>
Click here for Solution!
</summary>

![image](https://user-images.githubusercontent.com/120908587/221339074-3c74af26-7013-4a2a-92fc-528d86905c7b.png)

</details>


### 3 Budget level of customers ?

```sql
SELECT 
	 budget,
	 count(consumer_id) as Total_Customers
FROM 	 consumers
WHERE 	 budget is not null
GROUP BY budget
```

<details>
<summary>
Click here for Solution!
</summary>

![image](https://user-images.githubusercontent.com/120908587/221339384-96738d50-8517-4c3f-b2f7-ce27bd592ad8.png)

</details>


### 4 Total Smokers by Occupation ?

```sql
SELECT 
	 occupation,
	 count(consumer_id) as Smokers
FROM 	 consumers
WHERE smoker = 'Yes'
GROUP BY occupation
```

<details>
<summary>
Click here for Solution!
</summary>

![image](https://user-images.githubusercontent.com/120908587/221339410-df2a772c-baef-447e-ae78-2ad60a494303.png)

</details>


### 5 Drinking level of students ?

```sql
SELECT drink_level, count(consumer_id) as student_count
FROM 	 consumers
WHERE 	 occupation = 'Student' and occupation is not null
GROUP BY drink_level
```

<details>
<summary>
Click here for Solution!
</summary>

![image](https://user-images.githubusercontent.com/120908587/221339429-a128eb70-a1a3-4892-b5a5-49b4d95fd727.png)

</details>



### 6 Transportation methods of customers ?

```sql
SELECT 
	 transportation_method,
	 count(consumer_id) as Total_Customers
FROM 	 consumers
WHERE 	 transportation_method is not null	
GROUP BY transportation_method
Order BY Total_Customers DESC
```

<details>
<summary>
Click here for Solution!
</summary>

![image](https://user-images.githubusercontent.com/120908587/221339449-85f537c1-ba57-47b5-8279-5c282a98b2be.png)

</details>


### 7  Adding Age Bucket Column 

```sql
ALTER TABLE consumers 
ADD Age_Bucket Varchar(50)
```

### 8 Updating the Age Bucket column with case when condition

```sql
UPDATE consumers
SET age_bucket =
         CASE 
		      WHEN age > 60 then '61 and Above'
		      WHEN age > 40 then '41 - 60'	
		      WHEN age > 25 then '26 - 40'
		      WHEN age >= 18 then '18 - 25'
		      END
WHERE age_bucket is null					 ?
```

### 9  Total customers in each age bucket

```sql
SELECT 
	 age_bucket,
	 count(consumer_id) as Total_Customers
FROM 	 consumers
GROUP BY age_bucket
Order BY age_bucket
	
```

<details>
<summary>
Click here for Solution!
</summary>

![image](https://user-images.githubusercontent.com/120908587/221339559-6d08aeb5-9f18-4f50-952f-13fa73d38f52.png)

</details>


### 10 Total customers count & smokers count in each age percent 

```sql

SELECT 
	 age_bucket,
	 count(consumer_id) as total,
	 count(case when smoker = 'Yes' Then consumer_id end) as smokerscount
FROM 	 consumers
GROUP BY age_bucket
Order BY age_bucket	
```

<details>
<summary>
Click here for Solution!
</summary>

![image](https://user-images.githubusercontent.com/120908587/221339611-590caf69-b7a5-4b6d-93f7-e85e32e4e8a4.png)

</details>

### 11 What is the marital status distribution of customers in different state, and how does it vary based on their age and occupation?

```sql

select count(consumer_id),marital_status,age_bucket,state from consumers
group by marital_status,occupation,age_bucket,state
order by occupation desc
```

<details>
<summary>
Click here for Solution!
</summary>

![image](https://user-images.githubusercontent.com/120908587/221362896-a1e48120-e613-4273-9330-5a5fb0b3bb10.png)

</details>


### 12 How many customers are married, and what percentage of them belong to different age groups and occupations?

```sql

SELECT marital_status, age_group, occupation, 
       COUNT(*) AS count,
       ROUND(100.0 * COUNT(*) / SUM(COUNT(*)) OVER (PARTITION BY marital_status), 2) AS percentage
FROM (
  SELECT marital_status, 
         CASE 
           WHEN age BETWEEN 18 AND 25 THEN '18-25' 
           WHEN age BETWEEN 26 AND 35 THEN '26-35' 
           WHEN age BETWEEN 36 AND 45 THEN '36-45' 
           WHEN age BETWEEN 46 AND 55 THEN '46-55' 
           ELSE '55+' 
         END AS age_group,
         occupation
  FROM consumers
  WHERE marital_status = 'married'
) t
GROUP BY marital_status, age_group, occupation
ORDER BY count DESC
```

* OR

```sql
SELECT marital_status, age_group, occupation, 
       COUNT(*) AS count,
       100.0 * COUNT(*) / (SELECT COUNT(*) FROM customers WHERE marital_status = 'married') AS percentage
FROM (
  SELECT marital_status, 
         CASE 
           WHEN age BETWEEN 18 AND 25 THEN '18-25' 
           WHEN age BETWEEN 26 AND 35 THEN '26-35' 
           WHEN age BETWEEN 36 AND 45 THEN '36-45' 
           WHEN age BETWEEN 46 AND 55 THEN '46-55' 
           ELSE '55+' 
         END AS age_group,
         occupation
  FROM customers
  WHERE marital_status = 'married'
) t
GROUP BY marital_status, age_group, occupation
ORDER BY count DESC
```

<details>
<summary>
Click here for Solution!
</summary>

![image](https://user-images.githubusercontent.com/120908587/221362896-a1e48120-e613-4273-9330-5a5fb0b3bb10.png)

</details>


### 13 	What is the most common occupation among customers, and how does it vary based on their city, state, and country?


```sql
SELECT state, city, occupation, COUNT(*) AS count
FROM consumers c
GROUP BY  state, city, occupation
HAVING COUNT(*) >= ALL (
  SELECT COUNT(*) 
  FROM consumers
  WHERE  state = c.state AND city = c.city
  GROUP BY occupation
)
ORDER BY  state, city, count DESC
```
<details>
<summary>
Click here for Solution!
</summary>

![image](https://user-images.githubusercontent.com/120908587/221363701-33020a01-1841-4cee-b5cc-7a22a7fea855.png)

</details>


### 14 What is the average age of customers in different cities, states, and countries?


```sql
SELECT  state, city, AVG(age) AS average_age
FROM consumers
GROUP BY  state, city
ORDER BY  state, city

```
<details>
<summary>
Click here for Solution!
</summary>

![image](https://user-images.githubusercontent.com/120908587/221363893-857505ac-e02e-4607-87fd-d2d7adb60fa4.png)

</details>

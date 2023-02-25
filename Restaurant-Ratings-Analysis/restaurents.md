# 🍜 Case #1: restaurents Table 

## Solution

View the complete syntax [here](https://github.com/katiehuangx/8-Week-SQL-Challenge/blob/main/Case%20Study%20%231%20-%20Danny's%20Diner/SQL%20Syntax/Danny's%20Diner.sql).

***

###  These SQL queries analyzes the customers & their cuisines preferences. This helps to understand the types of customers & their preferences.


--- Q16) Total restaurants in each state
SELECT 
	 State,
	 count(restaurant_id) as Total_restaurant
FROM 	 restaurants
GROUP BY State
Order BY Total_restaurant DESC

--- Q17) Total restaurants in each city
SELECT 
	 city,
	 count(restaurant_id) as Total_restaurant
FROM 	 restaurants
GROUP BY city
Order BY Total_restaurant DESC
select * from restaurants
--- Q18) Restaurants count by alcohol service 
SELECT 
	 alcohol_service,
	 count(restaurant_id) as Total_restaurant
FROM 	 restaurants
GROUP BY alcohol_service
Order BY Total_restaurant DESC

--- Q19) Restaurants count by smoking allowed
SELECT 
	 smoking_allowed,
	 count(restaurant_id) as Total_restaurant
FROM 	 restaurants
GROUP BY smoking_allowed
Order BY Total_restaurant DESC

--- Q20) Alcohol & Smoking analysis
SELECT 
	 alcohol_service,smoking_allowed,
	 count(restaurant_id) as Total_restaurant
FROM 	 restaurants
GROUP BY alcohol_service,smoking_allowed
Order BY Total_restaurant DESC

--- Q21)Restaurants count by Price
SELECT 
	 price,
	 count(restaurant_id) as Total_restaurant
FROM 	 restaurants
GROUP BY price
Order BY Total_restaurant DESC

--- Q22)Restaurants count by parking
SELECT 
	 parking,
	 count(restaurant_id) as Total_restaurant
FROM 	 restaurants
GROUP BY parking
Order BY Total_restaurant DESC

--- Q23) Count of Restaurants by cuisines
SELECT 
        cuisine,
	count(restaurant_id) AS Total_restaurant
FROM 	restaurant_cuisines
GROUP BY cuisine
ORDER BY Total_restaurant DESC


--- Q26) Finding out count of each cuisine in each state

SELECT
	   b.cuisine,
	   SUM(CASE WHEN a.state = 'Morelos' Then 1 Else 0 END) AS Morelos,
	   SUM(CASE WHEN a.state = 'San Luis Potosi' Then 1 Else 0 END) AS San_Luis_Potosi,
	   SUM(CASE WHEN a.state = 'Tamaulipas' Then 1 Else 0 END) AS Tamaulipas
FROM 	   restaurants AS a
INNER JOIN restaurant_cuisines AS b
ON         a.restaurant_id = b.restaurant_id
GROUP BY   b.cuisine
ORDER BY   b.cuisine

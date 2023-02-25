𝗥𝗮𝘁𝗶𝗻𝗴𝘀 𝗔𝗻𝗮𝗹𝘆𝘀𝗶𝘀

This SQL queries analyzes the ratings given by customers to restaurants. This helps to understand the customer choice & restaurants performance better.
*/


--- Q27) Ratings given by customer for restaurants
SELECT 
	   b.consumer_id,
	   a.name as restaurant_name ,
	   b.overall_rating,
	   b.food_rating,
	   b.service_rating
FROM       restaurants as a 
INNER JOIN ratings as b
ON         a.restaurant_id = b.restaurant_id
ORDER BY   b.restaurant_id


--- Q28) Average ratings of each restaurant including it's cuisine type
SELECT 
	   a.name as restaurant_name ,
	   ROUND(AVG(b.overall_rating),2)as overall_Rating,
	   ROUND(AVG(b.food_rating),2)as food_rating,
	   ROUND(AVG(b.service_rating),2)as service_rating,
	   c.cuisine
FROM       restaurants as a 
INNER JOIN ratings as b
ON         a.restaurant_id = b.restaurant_id
INNER JOIN restaurant_cuisines AS c
ON         a.restaurant_id = c.restaurant_id
GROUP BY   a.name,c.cuisine
ORDER BY   a.name

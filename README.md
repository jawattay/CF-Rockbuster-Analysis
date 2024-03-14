<img width="329" alt="Rockbuster Stealth Logo" src="https://github.com/jawattay/CF-Rockbuster-Analysis/assets/162839921/72bd5985-b9c7-48a0-ba3c-ae809e42d7e9">

# **CF-Rockbuster-Analysis**
Analysis of Rockbuster data via PostgreSQL RDBMS (Relational Database Management System) as an analyst in the company's Business Intelligence department.
## **Objective**
Rockbuster Stealth LLC is a fictional movie rental service that used to have stores around the world. Now facing increasing competition from streaming platforms, I  assist Executives by loading existing data into a PostgreSQL RDBMS and then analyzing the company's current data to tailor a strategy for the upcoming launch of Rockbuster's streaming service.
## **Key Analysis Factors** 
-Which movies contributed the most/least to revenue gain?

-What was the average rental duration for all videos?

-Which countries are Rockbuster customers based in?

-Where are customers with a high lifetime value based?

-Do sales figures vary between geographic regions?

## **Data Sets**
-[Rockbuster Raw Data](https://www.postgresqltutorial.com/wp-content/uploads/2019/05/dvdrental.zip).

-[Rockbuster Final Data Sets](https://1drv.ms/u/s!Av6amgy3JU7viSm1MpWOpGEb7JRN?e=dDCx9r).

## **Deliverables**
-Presentation of Key Findings:[Tableau Vizualization](https://public.tableau.com/shared/T9W8CMBDG?:display_count=n&:origin=viz_share_link).

-Report: [Report PDF](https://1drv.ms/b/s!Av6amgy3JU7viB0vtArmEJHiezP5?e=2K7oez).

-Data Dictionary: [Data Dictionary PDF](https://1drv.ms/b/s!Av6amgy3JU7viB7RmVO5YjRQwcQd?e=MpHiq6).

-SQL Script Identifying Top 10 Countries

SELECT D.country,
       COUNT(country) AS customers
FROM customer A
INNER JOIN address B ON A.address_id = B.address_id
INNER JOIN city C ON B.city_id = C.city_id
INNER JOIN country D ON C.country_ID = D.country_ID
GROUP BY country
ORDER BY COUNT(country) DESC
LIMIT 10
![Top 10 Countries SQL Script](https://github.com/jawattay/CF-Rockbuster-Analysis/assets/162839921/32c5cdc5-a8f4-448e-82fe-c1ef28b4551f)

- SQL Script Identifying Top 10 Cities

SELECT D.country,
	   C.city,
       COUNT(customer_id) AS customer_count
FROM customer A
INNER JOIN address B ON A.address_id = B.address_id
INNER JOIN city C ON B.city_id = C.city_id
INNER JOIN country D ON C.country_ID = D.country_ID
WHERE country IN('India','China', 'United States', 'Japan', 'Mexico', 'Brazil', 'Russian Federation', 'Philippines', 'Turkey', 'Indonesia')
GROUP BY D.country,
	     C.city
ORDER BY customer_count DESC
LIMIT 10
![Top 10 Cities SQL Script](https://github.com/jawattay/CF-Rockbuster-Analysis/assets/162839921/42e3eac4-d9a5-4bf6-a7cb-d97dc33981bf)

- SQL Script Identifying Top 5 Customers

SELECT A.customer_id, A.first_name, A.last_name, C.city, D.country,
       SUM(E.amount) AS total_amount_paid
FROM customer A 
INNER JOIN address B ON A.address_id = B.address_id
INNER JOIN city C ON B.city_id = C.city_id
INNER JOIN country D ON C.country_id = D.country_id
INNER JOIN payment E ON A.customer_id = E.customer_id
WHERE C.city IN('Aurora', 'Acua', 'Citrus Heights', 'Iwaki', 'Ambattur', 'Shanwei', 
'So Leopoldo', 'Teboksary', 'Tianjin', 'Cianjur')
GROUP BY A.customer_id, A.first_name, A.last_name, C.city, D.country
ORDER BY total_amount_paid DESC
LIMIT 5
![Top 5 Customers SQL Script](https://github.com/jawattay/CF-Rockbuster-Analysis/assets/162839921/6a5eb39e-7ad5-4b1b-92af-a9b9647d8cf6)

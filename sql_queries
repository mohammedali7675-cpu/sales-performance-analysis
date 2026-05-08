SELECT *FROM sales;

SELECT SUM(sales) FROM sales;
SELECT 
SUM(sales) AS Total_Sales,
SUM(Profit) AS Total_Profit,
COUNT (Order_id) AS Total_Orders
FROM sales;

SELECT 
    DATE_TRUNC('month', Order_Date) AS Month,
    SUM(sales) AS Total_sales
FROM sales
GROUP BY month
ORDER BY Total_Sales DESC;
SELECT Sub_Category,discount
FROM sales
ORDER BY discount DESC
LIMIT 5;

SELECT Sub_Category, 
DATE_TRUNC('Month',Order_Date) AS Month,
MAX(discount) AS MAX_discount
FROM sales
GROUP BY DATE_TRUNC('Month',Order_Date),Sub_Category
ORDER BY MAX_discount DESC; 

SELECT Sub_Category,
TO_CHAR(DATE_TRUNC('Month',Order_Date),'Mon YYYY') AS month,
MAX(discount) AS MAX_discount,
MIN(discount) AS MIN_discount,
AVG(discount) AS AVG_discount
FROM Sales
WHERE DATE_TRUNC('Month',Order_Date)='2017-11-01'
GROUP BY DATE_TRUNC('Month',Order_Date),Sub_Category;

SELECT 
TO_CHAR(DATE_TRUNC('Month',Order_Date),'MM-YYYY') AS month,
COUNT(Order_ID) AS Total_Orders
FROM Sales
GROUP BY DATE_TRUNC('Month',Order_Date)
ORDER BY Total_Orders DESC;

SELECT 
TO_CHAR(DATE_TRUNC('Month',Order_Date),'MM-YYYY') AS month,
SUM(sales)/COUNT(DISTINCT(Order_ID)) AS avg_order_value
FROM sales
GROUP BY (DATE_TRUNC('Month',Order_Date))
ORDER BY avg_order_value DESC;

SELECT 
TO_CHAR(DATE_TRUNC('Month',Order_Date),'MM-YYYY') AS month,
SUM(Quantity) AS Total_quantity,
SUM(Quantity)::numeric / COUNT(DISTINCT Order_ID) AS Qty_per_order
FROM sales
GROUP BY DATE_TRUNC('Month',Order_Date)
ORDER BY Total_quantity DESC;

SELECT TO_CHAR(DATE_TRUNC('MONTH',Order_Date),'mm ,YYYY') AS Month,Sub_Category,
SUM(Sales) AS sales
FROM sales
WHERE Sub_Category IN
('Phones','Chairs','Tables','Copiers','Storage')
GROUP BY DATE_TRUNC('MONTH',Order_Date), Sub_Category
ORDER BY DATE_TRUNC('MONTH',Order_Date), Sub_Category;

SELECT*FROM(
SELECT TO_CHAR(DATE_TRUNC('MONTH',Order_Date),'mm ,YYYY') AS Month,Sub_Category,
SUM(Sales) AS Total_sales,
RANK() OVER(PARTITION BY DATE_TRUNC('MONTH',Order_Date)
            ORDER BY SUM(Sales) DESC )AS rnk
FROM sales
GROUP BY DATE_TRUNC('MONTH',Order_Date),Sub_Category
)t
WHERE rnk <=5
ORDER BY Month,rnk;

SELECT 
    CASE 
	  WHEN Sub_Category IN 
('Phones','Chairs','Storage','Tables','Copiers') THEN 'Top_products'
ELSE 'Other products' END AS Product_group,
SUM(Sales) AS Total_sales
FROM sales
GROUP  BY Product_group;

SELECT
    Sub_Category,
    ROUND(SUM(Sales),2) AS Total_sales
FROM sales
GROUP BY Sub_Category
ORDER BY Total_sales DESC;

SELECT 
    CASE 
	  WHEN Sub_Category IN 
('Phones','Chairs','Storage','Tables','Copiers') THEN 'Top_products'
ELSE 'Other products' END AS Product_group,
SUM(Profit) AS Total_profit
FROM sales
GROUP  BY Product_group;

SELECT
    Sub_Category,
    ROUND(SUM(Profit),2) AS Total_Profit
FROM sales
GROUP BY Sub_Category
ORDER BY Total_Profit ASC;

SELECT 
    DATE_TRUNC('month', Order_Date) AS Month,
    SUM(Profit) AS Total_Profit
FROM sales
GROUP BY month
ORDER BY Total_Profit DESC;


SELECT *
FROM (
    SELECT
        TO_CHAR(DATE_TRUNC('month', Order_Date),'Mon YYYY') AS Month,
        Sub_Category,
        ROUND(SUM(Profit),2) AS Profit,
        RANK() OVER (
            PARTITION BY DATE_TRUNC('month', Order_Date)
            ORDER BY SUM(Profit) DESC
        ) AS rnk
    FROM sales
    GROUP BY DATE_TRUNC('month', Order_Date), Sub_category
) t
WHERE rnk <= 5
ORDER BY Month, rnk;

SELECT
    TO_CHAR(DATE_TRUNC('month', Order_Date), 'MM,YYYY') AS Month,
    Sub_Category,
    ROUND(SUM(Profit),2) AS Total_Profit
FROM sales
GROUP BY DATE_TRUNC('month', Order_Date), Sub_Category
ORDER BY Total_Profit DESC;

SELECT
    TO_CHAR(DATE_TRUNC('month', Order_Date), 'MM YYYY') AS Month,
     Sub_Category AS Matching_Products
FROM sales
WHERE Sub_Category IN ('Phones','Chairs','Storage','Blinders','Accesories')
GROUP BY DATE_TRUNC('month', Order_Date), Sub_Category
ORDER BY DATE_TRUNC('month', Order_Date);

SELECT Sub_Category, 
DATE_TRUNC('Month',Order_Date) AS Month,
MAX(discount) AS MAX_discount
FROM sales
WHERE Sub_Category IN ('Phones','Chairs','Storage','Binders','Accessories')
GROUP BY DATE_TRUNC('Month',Order_Date),Sub_Category
ORDER BY MAX_discount DESC;


SELECT
    TO_CHAR(DATE_TRUNC('month', Order_Date),'MM YYYY') AS Month,
    SUM(Quantity) AS Qty,
    ROUND(SUM(Sales),2) AS Sales,
    ROUND(SUM(Profit),2) AS Profit,
    ROUND(AVG(Discount),2) AS Avg_Discount
	FROM sales
WHERE Sub_Category = 'Binders'
GROUP BY DATE_TRUNC('month', Order_Date)
ORDER BY DATE_TRUNC('month', Order_Date);

--loss analysis--
--loss sub category products--
SELECT Sub_Category,
       TO_CHAR(DATE_TRUNC('month', Order_Date),'MM YYYY') AS Month,
	   SUM(Profit) AS profits
FROM sales
WHERE DATE_TRUNC('month', Order_Date) IN ('2014-07-01','2015-01-01')
GROUP BY DATE_TRUNC('month', Order_Date),Sub_Category
ORDER BY DATE_TRUNC('month', Order_Date);



--CUSTOMER ANALYSIS--
SELECT 
Customer_ID,
SUM(Sales) AS SALES,
SUM(Profit) AS PROFIT
FROM 
sales
GROUP BY Customer_ID
ORDER BY SALES DESC
LIMIT 10;

SELECT
    Customer_ID,
    ROUND(SUM(Sales),2) AS Sales,
    ROUND(SUM(Profit),2) AS Profit
FROM sales
GROUP BY Customer_ID
HAVING SUM(Profit) < 0
ORDER BY Profit ASC;


SELECT
    Customer_ID,
    ROUND(MAX(Discount),2) AS MAX_Discount,
	 ROUND(AVG(Discount),2) AS AVG_Discount,
    ROUND(SUM(Profit),2) AS Profit,
	ROUND(SUM(Sales),2) AS sales
FROM sales
WHERE Customer_ID IN (
    SELECT Customer_ID
    FROM sales
    GROUP BY Customer_ID
    ORDER BY SUM(Sales) DESC
    LIMIT 10
)
GROUP BY Customer_ID,Sub_Category
ORDER BY Profit ASC;


SELECT
    Customer_ID,Sub_Category,Product_Name,
	SUM(Quantity) AS QUANTITY,
    ROUND(MAX(Discount),2) AS MAX_Discount,
	 ROUND(AVG(Discount),2) AS AVG_Discount,
    ROUND(SUM(Profit),2) AS Profit,
	ROUND(SUM(Sales),2) AS sales
FROM sales
WHERE Customer_ID IN (
    SELECT Customer_ID
    FROM sales
    GROUP BY Customer_ID
    ORDER BY SUM(Sales) DESC
    LIMIT 10
)
GROUP BY Customer_ID,Sub_Category,Product_Name
ORDER BY Profit ASC;


SELECT
    Customer_ID,Order_ID,Sub_Category,Product_Name,Region,
	SUM(Quantity) AS QUANTITY,
    ROUND(MAX(Discount),2) AS MAX_Discount,
	 ROUND(AVG(Discount),2) AS AVG_Discount,
    ROUND(SUM(Profit),2) AS Profit,
	ROUND(SUM(Sales),2) AS sales
FROM sales
GROUP BY Customer_ID,Order_ID,Sub_Category,Product_Name,Region
ORDER BY Profit ASC
LIMIT 10;

SELECT
Sub_Category,Shipmode,
SUM(Profit) AS profits,
SUM(Quantity) AS QUANTITY,
SUM(Sales) AS sales
FROM 
sales
GROUP BY Sub_Category,Shipmode
ORDER BY quantity DESC;

SELECT
Sub_Category,Product_Name,
SUM(Profit) AS profits,
SUM(Quantity) AS QUANTITY,
SUM(Sales) AS sales
FROM 
sales
GROUP BY Sub_Category,Product_Name
ORDER BY profits ASC;


# Shopify_Data_Science_Challenge
Winter 2022 Data Science Intern Challenge


Question 1: Given some sample data, write a program to answer the following: click here to access the required data set

On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 

a.Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. 

$3145.13 is obtained by simply calculating the avearge of "order_amount" column. In this case, since each shop only sells one model of shoe, the order amount is highly correlated to the total items column. If we use value_counts method on total items, we can see that 4983 orders include items numbering from 1 to 8 while 17 orders include 2000 items. That means 0.34% of the data are outliers and the distribution of order amount is highly positively skewed. So that taking the avearage of order amount can't give us a representative value for all the orders. A better way to evaluate this data would be to use a metric that is more robust in skewed distribution, in this case I think median of the order amount would be better represent the data.



b.What metric would you report for this dataset?

Median of order amount column.

c.What is its value?

284.0

Question 2: For this question you’ll need to use SQL. Follow this link to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

a.How many orders were shipped by Speedy Express in total?
Query:
SELECT COUNT(OrderID) FROM Orders O
INNER JOIN Shippers S
ON O.ShipperID = S.ShipperID
WHERE S.ShipperName = 'Speedy Express'

Answer:
54

b.What is the last name of the employee with the most orders?

Query:
SELECT E.LastName,COUNT(O.OrderID) as Order_Number from Employees E
INNER JOIN Orders O
ON E.EmployeeID = O.EmployeeID
GROUP BY E.LastName
ORDER BY Order_Number DESC

Answer:
Peacock

c.What product was ordered the most by customers in Germany?

Query:
SELECT P.ProductName,Count(DISTINCT O.OrderID) as Order_Count FROM Orders O
INNER JOIN Customers C
ON O.CustomerID = C.CustomerID
INNER JOIN OrderDetails OD
ON O.OrderID = OD.OrderID
INNER JOIN Products P
ON OD.ProductID = P.ProductID
WHERE C.Country = 'Germany'
GROUP BY P.ProductName
Order BY Order_Count DESC

Answer:
Gorgonzola Telino

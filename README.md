# SQL-Project
 DECLARE @SumOrd as money
 SET @SumOrd=(SELECT SUM(OrderCount) FROM tmpCustomer)

 SELECT *,
		(Ordercount/@SumOrd*100) AS [PERCENT],
		(CASE WHEN (Ordercount/@SumOrd*100)>40 THEN 'PREMIUM'
		WHEN (Ordercount/@SumOrd*100)<=40 AND (Ordercount/@SumOrd*100)>20 THEN 'MIDDLE'
		WHEN (Ordercount/@SumOrd*100)<20 THEN 'SMALL' END) AS RANKING
		FROM tmpCustomer
		WHERE ProductID IS NOT NULL
		ORDER BY CustomerID
    
    
    ---CREATE VIEW [dbo].[ProductView]
AS
SELECT  SalesLT.Product.ProductID, SalesLT.Product.Name AS ProductName, SalesLT.Product.ProductCategoryID, SalesLT.ProductCategory.Name AS ProductcategoryName, SalesLT.ProductModel.Name AS ProductModelName, 
                   SalesLT.ProductModelProductDescription.ProductDescriptionID, SalesLT.ProductModelProductDescription.Culture, SalesLT.ProductDescription.Description
FROM      SalesLT.ProductModelProductDescription INNER JOIN
                   SalesLT.ProductDescription ON SalesLT.ProductModelProductDescription.ProductDescriptionID = SalesLT.ProductDescription.ProductDescriptionID INNER JOIN
                   SalesLT.ProductModel ON SalesLT.ProductModelProductDescription.ProductModelID = SalesLT.ProductModel.ProductModelID INNER JOIN
                   SalesLT.Product ON SalesLT.ProductModel.ProductModelID = SalesLT.Product.ProductModelID INNER JOIN
                   SalesLT.ProductCategory ON SalesLT.Product.ProductCategoryID = SalesLT.ProductCategory.ProductCategoryID

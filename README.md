# Data_Analysis_BikeStore_Dashboard

## Dashboard
Tableau Public: [link](https://public.tableau.com/views/BikeStores_lip/Dashboard1?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

### Images (Please click to dashboard link for better experience):
![{E1A98F65-6445-470F-B9EF-D007C19AF52F}](https://github.com/user-attachments/assets/eb5c84ef-9f51-49bf-a1bc-ed979e2d8015)
![{749CEF7D-E3DF-414B-B3EB-D55255F1DEB4}](https://github.com/user-attachments/assets/3a2dd761-a598-4dc4-8b4b-9a837cffd865)
![{BFF308FA-F1F2-4396-BA74-87455EFBE9A8}](https://github.com/user-attachments/assets/a2de84fe-6754-4639-a6df-1417c64a5cd4)






## BigQuery
```sql
SELECT 
    ORD.ORDER_ID,
    CONCAT(CUS.FIRST_NAME, ' ', CUS.LAST_NAME) AS CUSTOMER_NAME,
    CUS.CITY,
    CUS.STATE,
    ORD.ORDER_DATE,
	SUM(ITE.QUANTITY) AS TOTAL_UNITS,
	SUM(ITE.QUANTITY * ITE.LIST_PRICE) AS REVENUE,
	PROD.PRODUCT_NAME,
	CAT.CATEGORY_NAME,
	STO.STORE_NAME,
	BRA.BRAND_NAME,
	CONCAT(STAF.FIRST_NAME, ' ', STAF.LAST_NAME) AS SALE_REP

FROM SALES.ORDERS AS ORD

JOIN SALES.CUSTOMERS AS CUS
ON ORD.CUSTOMER_ID = CUS.CUSTOMER_ID

JOIN SALES.ORDER_ITEMS AS ITE
ON ORD.ORDER_ID = ITE.ORDER_ID

JOIN PRODUCTION.PRODUCTS AS PROD
ON ITE.PRODUCT_ID = PROD.PRODUCT_ID

JOIN PRODUCTION.CATEGORIES AS CAT
ON PROD.CATEGORY_ID = CAT.CATEGORY_ID

JOIN SALES.STORES AS STO
ON ORD.STORE_ID = STO.STORE_ID

JOIN SALES.STAFFS AS STAF
ON ORD.STAFF_ID = STAF.STAFF_ID

JOIN PRODUCTION.BRANDS AS BRA
ON PROD.BRAND_ID = BRA.BRAND_ID

GROUP BY 
	ORD.ORDER_ID,
  CONCAT(CUS.FIRST_NAME, ' ', CUS.LAST_NAME),
  CUS.CITY,
  CUS.STATE,
  ORD.ORDER_DATE,
	PROD.PRODUCT_NAME,
	CAT.CATEGORY_NAME,
	STO.STORE_NAME,
	BRA.BRAND_NAME,
	CONCAT(STAF.FIRST_NAME, ' ', STAF.LAST_NAME)

```

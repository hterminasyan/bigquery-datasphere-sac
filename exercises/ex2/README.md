# Exercise 2 - Build and expose your data views on SAP Data Warehouse Cloud

In this exercise, you will construct and display data views on SAP Data Warehouse Cloud by utilizing predefined views from BigQuery and SAP S/4HANA. This process involves taking advantage of the rich data stored in BigQuery and incorporating it into your SAP Data Warehouse Cloud for analysis and reporting purposes. At the end of the exercise, the created views will be exposed and can be accessed from SAP Analytics Cloud to build interactive dashboards and generate meaningful insights. By combining the power of SAP Data Warehouse Cloud and SAP Analytics Cloud, you can gain a comprehensive view of your data and make informed decisions.


## Exercise 2.1 Creating a new view of "Product Sales Country" 

In this step of the exercise, you will build a new data view called **"Product Sales Country"** by combining and aggregating the "Sessions Hits by Country" and "Product Sales" views. This process involves joining the two views to create a comprehensive view of the sales data and aggregating it by country to provide insights into product sales trends by location. 

In the first step you will first create an inner join of the "Product SKU Transactions" and "Product Sales" data. This will allow you to combine the two views and create a comprehensive view of the sales data. Next, you will add a formula with a new calculated property to further enhance the insights generated from the data. Finally, you will join the projection with the "Hits by Session Country" table to provide a complete picture of product sales by location.

![Product Sales Country View](../../images/product-sales-country-view.png)


1. 👉 Open your [SAP Data Warehouse Cloud](https://ccebd5f3-3595-488d-846d-eda360636613.us10.hcs.cloud.sap/dwaas-ui/index.html#/home) using the provided credentials.
   
   Your user is associated with uniqe space (CATEGORY_MGMT_\<STUDENT>) where you can work and create your data artifacts. 
   
    ![New View](../../images/dwchome.png)


2. 👉 Go to **SAP DWC Data Builder** and create **New Graphical View**
    
    ![New View](../../images/newgraphview.png)


3. 👉 Open the **Shared Objects** from Repository, expand the views and drag and drop the following 3 views into the canvas
    - product_transactions_view
    - Product_Sales
    - hits_sessions_country_view
   
    ![New View](../../images/view1tables.png)


4. 👉 Drag and move **product_sku_transaction_view** on top of **Product_Sales** to create a **JOIN**
   
    ![Join](../../images/join1.png)


5. 👉 Define the following **JOIN** conditions:
    
    - Join Type: *Inner*
    - Mappings (see screenshot): DATE->DATE, Product_SKU->Product_SKU, transaction_id->transaction_id
   
    ![Join](../../images/join1map.png)


6. 👉 Keep the Projection columns unchanged
   
7. 👉 Add new **Calculated Column** (see screenshot below)
   
    ![Join](../../images/cc_column.png)

8. 👉 The idea of the calculated column is to have an additional DATE field with *String* data type, which is required for the next join. Add the following properties to the calculated column.
    - Business Name: *DATESTR*
    - Technical Name: *DATESTR*
    - Data Type: *String*
    - Lenght: *10*
    - Expression: *TO_NVARCHAR(DATE, 'YYYYMMDD')*
   
    ![Join](../../images/cc_column_properties.png)

9. 👉 Drag and move **Calculated Column** on top of **hits_session_country_view** to create the second **JOIN**
   
    ![Join](../../images/join2.png)

10. 👉 Define the following **JOIN** conditions:
    
    - Join Type: *Inner*
    - Mappings (see screenshot): DATESTR->DATET, Country->Country
   
    ![Join](../../images/join2map.png)

11. 👉 Finalyse the view by giving a name, semantic type and expose for consumption
    
    - Business Name: *Product_Sales_Country*
    - Technical Name: *Product_Sales_Country*
    - Semantic Usage: *Analytical Dataset*
    - Expose for Consumption: *On*
   
    ![Join](../../images/finalview1.png)

12. 👉 Create a new **Association**, search for the *"Time Dimension - Day"* and add it as a target.
    
    ![Join](../../images/association2.png)

13. 👉 Create the following mapping: **DATE->Date**
    
    ![Join](../../images/assoc_mapping2.png)

14. 👉 Save and deploy the **Product_Sales_Country** view
    
    ![Join](../../images/savedeploy.png)


## Exercise 2.2 Creating a new view of "Product Sales Country Discount" 

In this exercise, you will create a new data view called **"Product Sales Country Discount"**. This view will be created by joining it with the "Discount by Category Date" view, which is federated from the SAP S/4HANA system. This process involves combining the data from the two views to create a comprehensive view of product sales and discounts by country and date. The resulting "Product Sales Country Discount" view will provide valuable insights into sales trends, allowing you to make informed decisions about promotions and discounts. 

![Product Sales Country Discount](../../images/product_sales_country_discount.png)



1. 👉 Go to **SAP DWC Data Builder** and create **New Graphical View**
    
    ![New View](../../images/newgraphview.png)


2. 👉 Open the **Shared Objects** from Repository, expand the views and drag and drop the **"discount_by_category_date_view"** into the canvas.
3. 👉 Open the **Views** from the Repository and drop the **"Product_Sales_Country"** view into the canvas.
   
    ![New View](../../images/view2tables.png)

4. 👉 Drag and move **discount_by_category_date_view** on top of **Product_Sales_Country** to create a **JOIN**
   
    ![Join](../../images/join3.png)


5. 👉 Define the following **JOIN** conditions:
    
    - Join Type: *Left*
    - Mappings (see screenshot): Date->Date, Product_Category_Enhanced_Ecommerce->category
   
    ![Join](../../images/join1map.png)


6. 👉 Keep the Projection columns unchanged

7. 👉 Finalyse the view by giving a name, semantic type and expose for consumption
    
    - Business Name: *Product_Sales_Country_Discount*
    - Technical Name: *Product_Sales_Country_Discount*
    - Semantic Usage: *Analytical Dataset*
    - Expose for Consumption: *On*
   
    ![Join](../../images/finalview2.png)

8. 👉 Move **Sessions** and **Hits** attributes to **Measures**
    
    ![Join](../../images/att_meas.png)


9. 👉 Create a new **Association**, search for the *"Time Dimension - Day"* and add it as a target.
    
    ![Join](../../images/association2.png)

10. 👉 Create the following mapping: **DATE->Date**
    
    ![Join](../../images/assoc_mapping2.png)

11. 👉 Save and deploy the **Product_Sales_Country_Discount** view
    
    ![Join](../../images/savedeploy.png)



## Summary

The goal of Exercise 2 was to create two views in SAP Data Warehouse Cloud (DWC). The final view, "Product Sales by Country and Discount" was exposed and will be utilized by SAP Analytics Cloud to create a dashboard. This view provides insights into the sales of products by country and the discounts offered, which can be used to inform strategic business decisions. 

Continue to - [Exercise 3](../ex3/README.md)

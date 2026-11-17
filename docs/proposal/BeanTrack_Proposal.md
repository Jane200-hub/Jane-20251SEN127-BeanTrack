# BeanTrack: Smart Cafe Operations and Inventory Management System

**Student Name:** Kacyeye Igihozo Jane  
**Student ID:** 20251SEN127  
**Course:** INSY 8311 – Database Development with PL/SQL  
**Lecturer:** Eric Maniraguha

## 1. Problem Statement

Many small cafes manage their sales, stock and supplier information using notebooks or separate spreadsheets. This makes it difficult to monitor daily sales, know the quantity of available ingredients, track supplier deliveries and identify products that need restocking. Poor coordination between these activities can lead to stock shortages, unnecessary purchases, expired ingredients and financial losses.

BeanTrack is proposed to address these challenges by bringing the main cafe operations into one integrated database system.

## 2. Proposed Solution

BeanTrack will be developed using Oracle Database 21c and PL/SQL. It will manage product information, sales transactions, ingredient inventory, suppliers, purchases and stock movements.

When a sale is recorded, the system will use product recipes to calculate the ingredients required and update the corresponding stock quantities. It will also record received purchases and wasted ingredients. This will help maintain more accurate inventory records and provide useful information for daily management.

## 3. Data Source

The primary sales dataset will be the *Anonymous Transactional Dataset* by Engel, Gaol, Kurniawan and Budiharto (2026), obtained from Mendeley Data.

The dataset contains 53,820 sales transaction records and 96 product records collected from a real food and beverage MSME operating three outlets in Indonesia between January and September 2025. It is available under the Creative Commons Attribution 4.0 International licence (CC BY 4.0).

The original CSV files will be preserved in the project's `data/raw/` folder. Additional ingredient, recipe, supplier and stock information will require authorized data collection or clearly identified test records because these details are not included in the selected dataset. No personally identifying customer information will be used.

## 4. Planned Tables

The proposed database will contain the following tables:

1. PRODUCT_CATEGORIES – stores product categories.
2. MENU_ITEMS – stores cafe products and selling prices.
3. INVENTORY_ITEMS – stores ingredients and stock quantities.
4. SUPPLIERS – stores supplier information.
5. SUPPLIER_ITEMS – links suppliers to the ingredients they provide.
6. PURCHASE_ORDERS – stores purchase orders.
7. PURCHASE_ORDER_LINES – stores individual items in each order.
8. RECIPES – connects menu products to their required ingredients.
9. SALES – stores sales transaction details.
10. SALE_ITEMS – stores individual products sold in each transaction.
11. STOCK_MOVEMENTS – records stock increases and decreases.
12. WASTE_RECORDS – records expired, damaged or wasted ingredients.

## 5. Planned PL/SQL Features

The project will demonstrate the following PL/SQL features:

- Stored procedures for recording sales, receiving purchases and recording waste.
- Stored functions for calculating sales totals, stock values and reorder quantities.
- Packages for organizing related cafe operations.
- Explicit cursors for processing and reporting sales information.
- Triggers for recording inventory changes and maintaining audit information.
- Exception handling for insufficient stock and invalid transactions.
- Collections, BULK COLLECT and FORALL for processing multiple records efficiently.
- Bulk DML error handling to identify failed operations during batch processing.

## 6. Innovation

BeanTrack will include an interactive dashboard developed using Python Streamlit and connected to Oracle Database 21c.

The dashboard will display sales summaries, popular products, current stock levels, low-stock alerts and supplier information. Users will be able to record sales and view updated inventory information.

The main innovation is the connection between sales and ingredient inventory. Instead of updating stock manually after every sale, the system will use stored PL/SQL procedures and recipe information to calculate and record ingredient consumption automatically.

## 7. Expected Results

The expected result is an integrated cafe management system that improves sales recording, inventory monitoring, supplier coordination and stock control. It will also provide useful reports to support purchasing decisions and reduce avoidable stock losses.

## 8. References

Engel, M. M., Gaol, F. L., Kurniawan, A., & Budiharto, W. (2026). *Anonymous Transactional Dataset* (Version 2). Mendeley Data. https://doi.org/10.17632/kcgf45y24m.2

Engel, M. M., Gaol, F. L., Kurniawan, A., & Budiharto, W. (2026). Anonymous transactional dataset in a local food and beverages (F&B) micro-small-medium enterprise (MSME) for recommender systems. *Data in Brief, 65*, 112519. https://doi.org/10.1016/j.dib.2026.112519

Oracle. (2021). *Oracle Database PL/SQL Language Reference, 21c*. https://docs.oracle.com/en/database/oracle/oracle-database/21/lnpls/

United Nations Environment Programme. (2024). *Food Waste Index Report 2024*. https://wedocs.unep.org/handle/20.500.11822/45230

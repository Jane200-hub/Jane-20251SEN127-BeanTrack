# BeanTrack: Smart Cafe Operations and Inventory Management System

## Student Information
- **Student name:** Kacyeye Igihozo Jane
- **Student ID:** 20251SEN127
- **Course:** INSY 8311 – Database Development with PL/SQL
- **Project type:** Individual capstone project

## 1. Problem Statement
Small cafes need to manage daily sales, ingredients, stock levels, suppliers and purchases. When these activities are recorded manually or kept in separate records, it can be difficult to know how much stock is available, which ingredients need replenishment, how much is being wasted and which products are selling well. This can lead to stock shortages, unnecessary purchases, food waste and inaccurate business reports.

BeanTrack aims to address this problem by providing a centralized cafe operations system using Oracle Database and PL/SQL.

## 2. Project Objectives
The objectives of BeanTrack are to:
1. Record and manage cafe sales and the items sold.
2. Maintain records of menu products and the ingredients used to prepare them.
3. Track ingredient stock levels and stock movements.
4. Manage supplier information and purchase orders.
5. Update ingredient stock when purchases are received and when sales are processed.
6. Record damaged, expired or wasted ingredients.
7. Produce useful reports on sales, inventory, purchasing and waste.
8. Identify low-stock items that may need replenishment.

## 3. Data Source
The planned primary sales dataset is:

**Engel, M. M., Gaol, F. L., Kurniawan, A., & Budiharto, W. (2026). _Anonymous Transactional Dataset_ (Version 2) [Data set]. Mendeley Data.**

- Dataset: https://data.mendeley.com/datasets/kcgf45y24m/2
- DOI: https://doi.org/10.17632/kcgf45y24m.2
- Licence: CC BY 4.0 (credit must be given to the dataset authors).
- Reported contents: 53,820 anonymous sales transaction records and product information for 96 products from a real food-and-beverage business operating three outlets in Indonesia.

The dataset will support the sales and product sections of the project. It does not provide all the ingredient inventory, recipes, supplier, purchase-order and waste information required by BeanTrack. I will therefore seek permission to collect additional anonymized operational records from a participating cafe. Any records created only to test the application will be clearly labelled as synthetic test data and will not be presented as real business data.

No customer names, phone numbers, payment-card details or other personally identifying information will be collected or included.

## 4. Planned Innovation
The proposed innovation is a **live cafe management dashboard** connected to the Oracle database. It is planned using Python Streamlit and an Oracle database connection.

The dashboard is intended to:
- Display daily sales and sales summaries.
- Show best-selling menu items.
- Display current ingredient stock levels.
- Highlight ingredients that are running low.
- Show supplier and purchase-order information.
- Summarize recorded food waste.

The dashboard will call PL/SQL procedures for supported operations. For example, when a sale is recorded, the database will validate ingredient availability, save the sale and update the relevant stock records. The database—not just the dashboard—will enforce the business rules.

## 5. Planned Database Tables

| Table | Purpose |
|---|---|
| `PRODUCT_CATEGORIES` | Stores menu product categories. |
| `MENU_ITEMS` | Stores cafe products, descriptions and selling prices. |
| `INVENTORY_ITEMS` | Stores ingredients and their stock information. |
| `SUPPLIERS` | Stores supplier details. |
| `SUPPLIER_ITEMS` | Links suppliers to the ingredients they provide. |
| `PURCHASE_ORDERS` | Stores orders placed with suppliers. |
| `PURCHASE_ORDER_LINES` | Stores the ingredients and quantities in each purchase order. |
| `RECIPES` | Links menu items to the ingredients and quantities required to prepare them. |
| `SALES` | Stores sale transaction details. |
| `SALE_ITEMS` | Stores the menu items and quantities included in each sale. |
| `STOCK_MOVEMENTS` | Records stock received, used or adjusted. |
| `WASTE_RECORDS` | Records wasted, expired or damaged ingredients. |

The final table structures and relationships will be refined during the database-design phase.

## 6. Planned PL/SQL Features
The project is expected to demonstrate:
- **Stored procedures:** record sales, receive supplier purchases and record waste.
- **Stored functions:** calculate daily revenue, stock value and reorder quantities.
- **Packages:** group related cafe operations into a package such as `PKG_CAFE_OPERATIONS`.
- **Explicit cursors:** retrieve and process sales summaries or best-selling menu items.
- **Triggers:** maintain an audit trail when inventory records change.
- **Exception handling:** handle insufficient stock, invalid quantities and other transaction errors.
- **Collections and records:** store and process groups of related transaction data.
- **`BULK COLLECT` and `FORALL`:** retrieve and process multiple records efficiently.
- **Bulk DML error handling:** identify individual failures during batch operations.

## 7. Project Folder Structure
```text
beanTrack/
├── README.md
├── docs/
│   ├── research/
│   │   └── research_log.md
│   ├── proposal/
│   └── presentation/
└── data/
    ├── raw/
    └── cleaned/
```
Additional folders for database scripts, testing and the dashboard will be added in later project phases.

## 8. References
1. Engel, M. M., Gaol, F. L., Kurniawan, A., & Budiharto, W. (2026). _Anonymous Transactional Dataset_ (Version 2) [Data set]. Mendeley Data. https://doi.org/10.17632/kcgf45y24m.2
2. Engel, M. M., Gaol, F. L., Kurniawan, A., & Budiharto, W. (2026). Anonymous transactional dataset in a local food and beverages (F&B) micro-small-medium enterprise (MSME) for recommender systems. _Data in Brief, 65_, 112519. https://doi.org/10.1016/j.dib.2026.112519
3. Ramadhan, A. N., & Simatupang, T. M. (2012). Determining inventory management policy for perishable materials in Roemah Keboen Restaurant. _Procedia - Social and Behavioral Sciences, 65_, 992–999. https://doi.org/10.1016/j.sbspro.2012.11.232
4. Salas Puente, M. F., Vera, C., & Campoverde, R. (2026). Inventory optimization and working capital efficiency in a small-scale restaurant: An applied ABC–JIT case study. _LACCEI, 1_(14). https://doi.org/10.18687/LACCEI2026.1.1.2600
5. United Nations Environment Programme. (2024). _Food Waste Index Report 2024: Think eat save—Tracking progress to halve global food waste_. https://wedocs.unep.org/handle/20.500.11822/45230
6. Food and Agriculture Organization of the United Nations. (n.d.). _Food Loss and Waste Database_. https://www.fao.org/datalab/filling-data-gaps/food-loss-and-waste-database/
7. Square. (n.d.). _Manage ingredient inventory with Square Restaurant Inventory_. Square Support. https://api.squareup.com/help/us/en/article/8610-manage-ingredient-inventory-with-square-restaurant-inventory
8. Oracle Corporation. (2024). _Oracle Database PL/SQL Language Reference, 21c_ (F31827-07). https://docs.oracle.com/en/database/oracle/oracle-database/21/lnpls/

---
**Project status:** Phase 0 – research and proposal preparation.

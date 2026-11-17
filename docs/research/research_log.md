# BeanTrack – Research Log

**Project Title:** BeanTrack: Smart Cafe Operations and Inventory Management System

**Student Name:** Kacyeye Igihozo Jane

**Student ID:** 20251SEN127

**Course:** INSY 8311 – Database Development with PL/SQL

## 1. Research Sources

| # | Source (APA) | Type | Link | Key finding | Gap it shows |
|---|---|---|---|---|---|
| 1 | Engel, M. M., Gaol, F. L., Kurniawan, A., & Budiharto, W. (2026). *Anonymous Transactional Dataset* (Version 2). Mendeley Data. https://doi.org/10.17632/kcgf45y24m.2 | Real-world dataset | https://data.mendeley.com/datasets/kcgf45y24m/2 | Contains historical sales transactions and product information collected from a real food and beverage business operating multiple outlets in Indonesia. | Provides sales and product information but does not include ingredient inventory, supplier records, purchase orders or wastage information. |
| 2 | Engel, M. M., Gaol, F. L., Kurniawan, A., & Budiharto, W. (2026). Anonymous transactional dataset in a local food and beverages (F&B) micro-small-medium enterprise (MSME) for recommender systems. *Data in Brief, 65*, 112519. https://doi.org/10.1016/j.dib.2026.112519 | Research/data article | https://doi.org/10.1016/j.dib.2026.112519 | Explains how real business transaction records were collected, cleaned and prepared for research. | Focuses on transactional data and recommendation systems rather than complete cafe inventory and supplier management. |
| 3 | Ramadhan, A. N., & Simatupang, T. M. (2012). Determining inventory management policy for perishable materials in Roemah Keboen Restaurant. *Procedia - Social and Behavioral Sciences, 65*, 992–999. https://doi.org/10.1016/j.sbspro.2012.11.232 | Research paper | https://doi.org/10.1016/j.sbspro.2012.11.232 | Discusses inventory decisions for perishable restaurant materials and how stock management affects waste and operating costs. | Shows the importance of better stock monitoring and ordering decisions. BeanTrack will connect stock records with sales and reorder information. |
| 4 | United Nations Environment Programme. (2024). *Food Waste Index Report 2024*. https://wedocs.unep.org/handle/20.500.11822/45230 | International report | https://wedocs.unep.org/handle/20.500.11822/45230 | Highlights the importance of measuring food waste in food service, retail and household sectors to support waste reduction. | Supports the need to record and monitor waste. BeanTrack will include waste records to help identify losses in cafe operations. |
| 5 | Square. (n.d.). *Capabilities: Square for Restaurants*. https://squareup.com/us/en/restaurants/capabilities | Existing system | https://squareup.com/us/en/restaurants/capabilities | Provides restaurant features such as sales processing, menu management, inventory tracking and order management. | Demonstrates that integrated restaurant management is possible. BeanTrack will provide a student-developed Oracle PL/SQL implementation focused on cafe operations. |
| 6 | Oracle. (2021). *Oracle Database PL/SQL Language Reference, 21c*. https://docs.oracle.com/en/database/oracle/oracle-database/21/lnpls/ | Technical documentation | https://docs.oracle.com/en/database/oracle/oracle-database/21/lnpls/ | Explains PL/SQL programming, procedures, functions, packages, triggers, collections and bulk processing using BULK COLLECT and FORALL. | Provides the technical foundation, but does not provide a ready-made cafe management application. BeanTrack will apply these features to practical cafe operations. |

## 2. Data-use and Verification Notes

The Mendeley dataset will be used as the primary source of real sales data for BeanTrack.

- Attribute the dataset to its original authors.
- Retain the Creative Commons Attribution 4.0 International (CC BY 4.0) licence information when using or adapting the data.
- Preserve the original downloaded CSV files in the `data/raw/` folder.
- Store any cleaned or modified versions separately.
- Do not include personal information that identifies real individuals.

### 2.1 Dataset Verification

The Anonymous Transactional Dataset published by Engel, Gaol, Kurniawan and Budiharto (2026) was selected as the primary source of real sales data for BeanTrack. The dataset describes historical transactions collected from a real food and beverage MSME operating three outlets in Indonesia.

The downloaded dataset contains two CSV files:

- **Transactions.csv:** 53,820 transaction records covering January to September 2025.
- **Products.csv:** 96 product records containing product names, variants, categories, prices and descriptions.

The files were inspected using Python. Both files contained no missing values or duplicate complete records. The transaction file contained 53,820 unique receipt numbers.

**Dataset research gap:** The dataset provides sales and product information but does not include ingredient stock levels, supplier records, purchase orders, recipes or wastage records. BeanTrack will address these additional operational requirements through its proposed database design and further authorized data collection or clearly labelled test records.

**Data licence:** Creative Commons Attribution 4.0 International (CC BY 4.0). The dataset must be properly attributed to its authors.

## 3. Overall Research Gap

The reviewed sources show that restaurant and cafe operations involve several connected activities, including sales recording, inventory control, supplier management and food-waste monitoring. Existing systems provide some of these functions, while the selected real-world dataset mainly covers sales transactions and product information.

BeanTrack will address this gap by developing an integrated Oracle database application that connects sales, products, ingredient inventory, suppliers, purchases and waste records. PL/SQL procedures, functions, packages, triggers and bulk processing will support the main business operations.

The proposed system will also include a dashboard to help users monitor sales, stock levels, supplier information and inventory alerts.

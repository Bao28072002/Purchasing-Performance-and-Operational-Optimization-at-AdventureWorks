# Purchasing Performance and Operational Optimization at AdventureWorks | Power BI

![Image](https://github.com/user-attachments/assets/3cbe74ea-1dbf-43c0-a860-fd5e16151c35)

**Author:** Lê Gia Bảo

**Date:** July 2025

**Tools Used:** Power BI

## 📑 Table of Contents  
1. [📌 Background & Overview](#-background--overview)  
2. [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)  
3. [🧠 Design Thinking Process](#-design-thinking-process)  
4. [📊 Key Insights & Visualizations](#-key-insights--visualizations)  
5. [🔎 Final Conclusion & Recommendations](#-final-conclusion--recommendations)

---

## 📌 Background & Overview  

**Objective:**

**📖 What is this project about?**

This project analyzes purchasing activities at **AdventureWorks** to support better operational decisions. The Power BI dashboard focuses on:

- **Purchasing Performance**: Monitoring back order rates to ensure timely and sufficient supply for manufacturing needs.  
- **Cost Optimization**: Evaluating average purchase order costs to identify savings opportunities and improve procurement efficiency.


**👤 Who is this project for?**

This dashboard is designed for key stakeholders involved in the purchasing process at **AdventureWorks**, including:

- **Purchasing Manager**: To monitor supplier performance, order fulfillment, and spot procurement issues early.  
- **Purchasing Executive**: To track purchasing KPIs, ensure compliance with procurement strategies, and manage day-to-day operations efficiently.  
- **Board of Directors (BOD)**: To gain high-level insights into purchasing efficiency and cost control for strategic decision-making.

**❓Business Questions:**

- Are we experiencing high back order rates that may impact production timelines?  
- How cost-effective are our purchase orders across different vendors and materials?  
- Which vendors are consistently delivering on time and within budget?  
- Are there any unusual spikes in purchasing cost that need further investigation?  
- How can we improve procurement planning to reduce delays and optimize costs?

**🎯Project Outcome:**

The project provided insights into **order handling**, **cost control**, and **vendor performance**, identifying key improvement areas to optimize operations.

#### Key Results:
- Improved order management during peak seasons to reduce backorder risks.
- Optimized PO cost management, ensuring stability throughout the year.
- Mitigated vendor risks by renegotiating contracts with high-cost suppliers.
- Enhanced product classification for better resource allocation and spending tracking.

#### Outcome:
The project enabled data-driven decisions, improving operational efficiency, cost-effectiveness, and vendor management.

# 📂 Dataset Description & Data Structure

### **📌 Data Source** 
- **Source**: Kaggle - Dataset of AdventureWorks
- **Size**: The **Purchase_OrderDetails** table contains **8,845** records.  
- **Format**: Pbix

### 📊 **Data Structure & Relationships**  

#### 1️⃣ **Tables Used:**  
The dataset consists of **7 main tables** used to build the purchasing dashboard:

- 📦 **Fact_Purchasing_OrderDetail** – Line-level order details.

<details>
<summary><strong>Table 1: Fact_Purchasing_OrderDetail</strong></summary>

| Column Name             | Description                                  |
|-------------------------|----------------------------------------------|
| `OrderQty`              | Quantity ordered                             |
| `ReceivedQty`           | Quantity received                            |
| `RejectedQty`           | Quantity rejected                            |
| `StockedQty`            | Quantity stocked                             |
| `LeadTime_Days`         | Lead time in days                            |
| `DelayDays`             | Number of delay days                         |
| `DueDate`, `OnTime`     | Delivery due date and on-time flag           |
| `IsBackorderedFlag`     | Indicates if the item was backordered        |
| `UnitPrice`             | Unit price of the item                       |
| `PurchaseOrderDetailID` | Line item identifier                         |
| `PurchaseOrderID`, `ProductID` | Foreign keys to orders and products     |

</details>

- 🏷️ **Fact_Product_Inventory** – Current inventory levels.

<details>
<summary><strong>Table 2: Fact_Product_Inventory</strong></summary>

| Column Name           | Description                                |
|------------------------|--------------------------------------------|
| `Quantity`             | Current inventory quantity                 |
| `Below Reorder Flag`   | Indicates if inventory is below reorder level |
| `BelowSafetyStock`     | Indicates stock is below safety threshold  |
| `OutOfStockProducts`   | Out of stock status                        |
| `ProductID`            | Foreign key to product                     |

</details>

- 🧾 **Dim_Product_Product** – Product master data.

<details>
<summary><strong>Table 3: Dim_Product_Product</strong></summary>

| Column Name           | Description                                |
|------------------------|--------------------------------------------|
| `ProductID`            | Unique product identifier                  |
| `Name`, `Class`, `Style` | Product characteristics                   |
| `SafetyStockLevel`     | Safety stock value                         |
| `ReorderPoint`         | Reorder threshold                          |
| `ListPrice`, `StandardCost` | Price and cost info                  |
| `ProductSubcategoryID` | Foreign key to product taxonomy            |

</details>

- 📄 **Dim_Purchasing_OrderHeader** – Order-level metadata.

<details>
<summary><strong>Table 4: Dim_Purchasing_OrderHeader</strong></summary>

| Column Name         | Description                                 |
|----------------------|---------------------------------------------|
| `PurchaseOrderID`    | Header-level order ID                       |
| `OrderDate`, `ShipDate` | Order creation and shipping date         |
| `VendorID`           | Foreign key to vendor                       |
| `TotalDue`, `Freight`, `SubTotal` | Order-level cost details      |

</details>

- 🧑‍💼 **Dim_Purchasing_Vendor** – Vendor master data.

<details>
<summary><strong>Table 5: Dim_Purchasing_Vendor</strong></summary>

| Column Name             | Description                            |
|--------------------------|----------------------------------------|
| `VendorID`               | Unique vendor ID                       |
| `Name`, `AccountNumber`  | Vendor info                            |
| `PreferredVendorLabel`   | Whether vendor is preferred            |
| `CreditRating`           | Vendor's credit rating                 |

</details>

- 🔗 **Dim_Purchasing_ProductVendor** – Product-vendor mapping.

<details>
<summary><strong>Table 6: Dim_Purchasing_ProductVendor</strong></summary>

| Column Name           | Description                              |
|------------------------|------------------------------------------|
| `ProductID`            | Linked product                           |
| `VendorID`             | Linked vendor                            |
| `MinOrderQty`, `MaxOrderQty` | Order quantity boundaries        |
| `StandardPrice`        | Standard unit cost                       |
| `AverageLeadTime`      | Vendor delivery time in days             |

</details>

- 🧱 **Dim_Product_ProductTaxonomy** – Product categories.

<details>
<summary><strong>Table 7: Dim_Product_ProductTaxonomy</strong></summary>

| Column Name           | Description                                |
|------------------------|--------------------------------------------|
| `ProductID`            | Product reference                          |
| `Category`, `Subcategory` | Product hierarchy                      |

</details>

- 🗂️ **Dim_Product_ProductTable** – Product category and hierarchy.

<details>
<summary><strong>Table 8: Dim_Product_ProductTable</strong></summary>

| Column Name             | Description                         |
|--------------------------|-------------------------------------|
| `ProductID`              | Linked product                      |
| `ProductCategoryID`      | Category reference                  |
| `ProductSubcategoryID`   | Subcategory reference               |
| `Category`               | Product category name               |
| `Subcategory`            | Product subcategory name            |

</details>

#### 2️⃣ Data Relationships:

![Image](https://github.com/user-attachments/assets/5d697c87-7628-4d70-b1d4-3163e44ae1fc)

| **From Table**                  | **To Table**                     | **Join Key**                | **Relationship Type**                                      |
|--------------------------------|----------------------------------|-----------------------------|------------------------------------------------------------|
| `Fact_Purchasing_OrderDetail`  | `Dim_Purchasing_OrderHeader`     | `PurchaseOrderID`           | Many-to-One (many order lines per order header)            |
| `Fact_Purchasing_OrderDetail`  | `Dim_Product_Product`            | `ProductID`                 | Many-to-One (many order lines for one product)             |
| `Fact_Purchasing_OrderDetail`  | `Dim_Order_Date`                 | `DueDate` / `ModifiedDate`  | Many-to-One (orders map to one date)                       |
| `Dim_Purchasing_OrderHeader`   | `Dim_Purchasing_Vendor`          | `VendorID`                  | Many-to-One (multiple orders per vendor)                   |
| `Dim_Purchasing_ProductVendor` | `Dim_Purchasing_Vendor`          | `VendorID`                  | Many-to-One (vendor supplies many products)                |
| `Dim_Purchasing_ProductVendor` | `Dim_Product_Product`            | `ProductID`                 | Many-to-One (vendor offers multiple products)              |
| `Dim_Product_Product`          | `Dim_Product_ProductTaxonomy`    | `ProductSubcategoryID`      | Many-to-One (each product belongs to one subcategory)      |
| `Fact_Product_Inventory`       | `Dim_Product_Product`            | `ProductID`                 | Many-to-One (each inventory record linked to a product)    |

# 🧠 Design Thinking Process

### 1️⃣ Empathize

![Image](https://github.com/user-attachments/assets/e69224c7-8272-45b7-9341-2e73aee0be8b)

![Image](https://github.com/user-attachments/assets/dfd3a807-480c-4382-b57d-71744fdf4e92)

![Image](https://github.com/user-attachments/assets/92e0d009-b0fe-441d-9901-86ece9a87ca6)

### 2️⃣ Define point of view 

![Image](https://github.com/user-attachments/assets/9c8b2fd9-4bf6-47cc-878f-802d5f67eb66)

![Image](https://github.com/user-attachments/assets/7328ee67-4acf-4094-9c7e-ce2c322e54fe)

### 3️⃣ Ideate

![Image](https://github.com/user-attachments/assets/a1596b12-a5c2-4008-95fd-b5f6d80ed7f8)

![Image](https://github.com/user-attachments/assets/a2c1aa14-8610-4927-b839-19261dc8ee31)

### 4️⃣ Prototype and review

This part is in the dashboard

# 📊 Key Insights & Visualizations

### 🔍 Dashboard Preview

### 📋 I. Executive Summary

![Image](https://github.com/user-attachments/assets/c75e1741-a924-43c9-bd16-1452abafb41e)

### 📌 Key Findings:

#### **1. Total Order, Late Orders and Back Order Rate (%)**
- Total orders peaked in **May–June** (456 orders). Both **Late Orders** and **Back Order Rate** reached their highest in **June–July (~10.5%)**. Steady decline in these two metrics after August.

-> **Demand peaks mid-year**, causing strain, but ops performance improves clearly in Q4.

#### **2. AVG Purchase Order Cost Trend**
- Average PO cost fluctuated between **$6.3K and $7.8K**. Peaked in **March**, dropped sharply by **October**. The Last Month (LM) line remains stable around **$7.0K–$7.2K**.

-> PO costs **fluctuate seasonally**, with stronger control toward year-end.

#### **3. Cumulative PO Cost and Cumulative PO Count**
- Cumulative PO Cost steadily increased to **$64M by August**, followed by a sharp drop. This year’s PO count is significantly lower compared to last year.

-> Likely shift to batch purchasing, **fewer but larger POs**.

#### **4. Top 3 Vendor Pricing vs Market Average Over Time**
- **Chicago City** consistently charges higher than **market average** (~35.5 vs 34.3–34.7). **SUPERSALES** and **Custom Framers** offer **lower-than-market** pricing with consistent trends.

-> **Heavy spend on higher-cost vendors**, suggesting a strategic choice.

#### **5. Total PO by Month and Category**
- PO volume peaked in **August**, dropped drastically afterward. The **(Blank)** category dominates, while other categories like Accessories and Components are minimal.

-> **Product classification is incomplete**, limiting detailed tracking.

#### **6. Total Purchase Spend by Sub-Category**
- The sub-category **"(Blank)"** represents the **highest total purchase spend ($22M)**, dwarfing all other defined categories. Categories like **Pedals and Tires and Tubes** show substantial spending **($13M each)**, others like **Jerseys, Shorts, Vests, and Bib-Shorts** have considerably **lower spending ($1M or less).**

-> Spending is **concentrated in Pedals, Tires, and large unclassified "(Blank)"** amounts

### 📈 II. Product Analysis

![Image](https://github.com/user-attachments/assets/da07a0f4-da91-4480-9d7d-a9b89e608562)

### 📌 Key Findings:

#### **1. Purchase Volume & Average Price**
- Purchase volume peaked during **April–August** with strong growth, then slightly declined in **October**.
- Meanwhile, the **average purchase price** showed a steady increase from **34.1** to **35.5**, even as volume tapered off.

#### **2. Inventory Turnover**
- **Inventory turnover** reached its highest point in **June–July** (23K), reflecting strong mid-year demand or movement.
- However, from **September** onward, turnover dropped sharply, indicating slower stock movement.

#### **3. SKUs Below Thresholds**
- Several key SKUs are currently below safety stock thresholds, notably **HL Mountain Frame (145 SKUs)** and **ML Touring Frame (98 SKUs)**.
- This raises the risk of stockouts if demand picks up or new orders surge.

#### **4. Product & Finished Goods Overview**
- Finished goods ratio fluctuates between **33–47%**, indicating stock imbalance across product groups.
- Some groups show lower finished goods levels, which could impact order fulfillment capability.

#### **5. Total Spend by Product**
- Spending is heavily concentrated on frame lines, with **HL Mountain Frame** leading at **$1.13M**, followed by **ML Touring Frame ($1.01M)**.
- Other product lines show significantly lower total spend.

#### **6. PO & Backorder Rate**
- Although total POs for **Components** are not large, the backorder rate is the highest (**18%**), signaling potential supply gaps from vendors.

#### **7. Inventory Status**
- Many SKUs are currently flagged as **Overstocked**, and the system recommends **Pausing Purchasing** for these items to prevent inventory buildup.

### III. 🤝 Vendor Performance

![Image](https://github.com/user-attachments/assets/27a04562-6258-4915-bc6a-f7ce96745722)

### 📌 Key Findings:

#### **1. PO Cost Variance & Pareto Analysis**
- **Superior Bicycles** leads with **20.6%** of total PO cost variance, indicating a significant impact on purchasing costs.
- The top 5 vendors contribute over **50%** of total variance, showing a high concentration that requires closer cost control.

#### **2. Vendor Spend & Backorder Risk**
- **Superior Bicycles** has the highest spend (**$4.56M**) but also shows a high backorder rate (**20%**).
- **Chicago City Saddles** records the **highest backorder (21.6%)**, signaling a major fulfillment risk.
- In contrast, vendors like **Victory Bikes (11.8%)** and **Inline Accessories (9.8%)** have lower backorder rates, supporting more stable supply.

#### **3. Average PO Cost & Price Trend**
- **Superior Bicycles** also leads in **average PO cost ($45.5K)**, with an upward price trend over the past 6 months.
- Other vendors such as **Inline Accessories ($34.4K)** maintain more stable pricing, helping mitigate price volatility risks.

#### **4. Vendor Segmentation by Spend & Rating**
- **Victory Bikes** and **Proseware, Inc.** are positioned favorably with balanced spend and higher ratings.
- Meanwhile, **Chicago City Saddles** and **Superior Bicycles**, despite their high spend, also carry higher fulfillment risks and need tighter monitoring.

#### **5. Preferred Vendor Pipeline**
- Currently, **91%** of the purchasing pipeline is allocated to **preferred vendors**, ensuring alignment with strategic partners but also requiring close tracking of their performance.

# 🔎 Final Conclusion & Recommendation

| **Aspect**                     | **Insight**                                                                                                      | **Recommendation**                                                                                       |
|---------------------------------|------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| **Order & PO Performance**      | - **Peak demand during May–June** creates significant pressure on operations, with **Late Orders and Back Order Rate** reaching their highest in June–July (~10.5%). After August, performance improves. | - Improve **order handling during peak seasons** to reduce pressure. <br> - Optimize **processing for at-risk orders**. |
| **PO Cost & Trends**            | - **PO costs fluctuate** throughout the year, peaking in March and dropping sharply by October. Despite fluctuations, PO costs stabilize around $7.0K–$7.2K by year-end. | - Continue to **control PO costs** tightly, especially at year-end. <br> - **Monitor cost fluctuations** and adjust procurement strategy proactively to avoid sudden cost spikes. |
| **Vendor Performance & Risks**  | - Major suppliers like **Chicago City** and **Superior Bicycles** not only have **high costs** but also present significant **backorder risks**, with backorder rates of **21.6% and 20%** respectively, posing delivery risks. | - **Renegotiate prices** with high-cost suppliers or consider switching suppliers. <br> - Improve delivery processes with high backorder suppliers or reassess suppliers if backorder rates remain high. |
| **Product & Inventory Management** | - **Incomplete product classification** makes it difficult to track spending accurately. The **Blank** product line accounts for the highest spending ($22M), while categories like **Jerseys** and **Vests** show low spending. | - Improve **product classification** for better tracking of spending and to avoid omissions. <br> - Focus on high-spending product lines like **Pedals** and **Tires & Tubes** to optimize resource allocation and purchasing strategy. |

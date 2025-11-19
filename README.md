# Purchasing Performance and Operational Optimization at AdventureWorks | Power BI

<img width="3999" height="3999" alt="image" src="https://github.com/user-attachments/assets/e1ba8a09-734b-44c8-af94-e996f824482e" />

**Author:** Lê Gia Bảo

**Date:** August 2025

**Tools Used:** Power BI

## 📑 Table of Contents  
1. [📌 Background & Overview](#-background--overview)  
2. [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)  
3. [🧠 Design Thinking Process](#-design-thinking-process)  
4. [📊 Key Insights & Visualizations](#-key-insights--visualizations)  
5. [🔎 Final Conclusion & Recommendations](#-final-conclusion--recommendation)

---

## 📌 Background & Overview  

**Objective:**

**📖 What is this project about?**

This project analyzes purchasing activities at **AdventureWorks** to support data-driven operational decisions. The Power BI dashboard focuses on two main areas:

- **Purchasing Performance** – Tracking back-order rates to ensure timely and sufficient supply for production.  
- **Cost Optimization** – Evaluating average purchase order costs to identify saving opportunities and improve procurement efficiency.

**👤 Who is this project for?**

This dashboard is designed for key stakeholders involved in the purchasing process at **AdventureWorks**, including:

- **Purchasing Manager** – Monitor supplier performance, order fulfillment, and detect issues early.  
- **Purchasing Executive** – Track purchasing KPIs, ensure compliance with procurement strategy, and manage day-to-day operations.  
- **Board of Directors (BOD)** – Access high-level insights into purchasing efficiency and cost control for strategic decisions.

**❓Business Questions:**

- Are back-order rates high enough to affect production timelines?  
- How cost-efficient are purchase orders across different vendors and materials?  
- Which vendors consistently deliver on time and within budget?  
- Are there unusual spikes in purchasing costs that require deeper investigation?  
- What improvements can strengthen procurement planning to reduce delays and optimize costs?

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

<img width="1318" height="811" alt="image" src="https://github.com/user-attachments/assets/61b12c90-5a5a-4de6-8da9-222f74e12564" />


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



### 2️⃣ Define point of view 



### 3️⃣ Ideate



### 4️⃣ Prototype and review

This part is in the dashboard

# 📊 Key Insights & Visualizations

### 🔍 Dashboard Preview

### 📋 I. Executive Summary

![Image](https://github.com/user-attachments/assets/c75e1741-a924-43c9-bd16-1452abafb41e)

### 📌 Key Findings:

#### 1. Total Orders, Late Orders, and Back Order Rate (%)
- Orders peaked in **May–June** (456 orders), with **Late Orders** and **Back Order Rate** highest in **June–July (~10.5%)**. Both metrics steadily declined after August.

→ **Mid-year demand spikes** caused pressure, but operational performance improved noticeably in Q4.

#### 2. Average Purchase Order Cost Trend
- Average PO cost ranged between **$6.3K and $7.8K**, peaking in **March** and dropping sharply by **October**. The Last Month (LM) line stayed stable around **$7.0K–$7.2K**.

→ PO costs **fluctuate seasonally**, with better control toward year-end.

#### 3. Cumulative PO Cost and Count
- Cumulative PO cost rose steadily to **$64M by August**, then declined sharply. This year’s PO count is **lower than last year**.

→ Indicates a shift toward **fewer but larger POs**, likely batch purchasing.

#### 4. Top 3 Vendor Pricing vs Market Average
- **Chicago City** consistently charges above the market (~35.5 vs 34.3–34.7), while **SUPERSALES** and **Custom Framers** offer **lower-than-market** prices consistently.

→ The company **spends heavily on higher-cost vendors**, likely as a strategic decision.

#### 5. Total PO by Month and Category
- PO volume peaked in **August** and dropped sharply afterward. The **(Blank)** category dominates; other categories like Accessories and Components are minor.

→ **Incomplete product classification** limits detailed tracking.

#### 6. Total Purchase Spend by Sub-Category
- The **"(Blank)"** sub-category accounts for the **largest spend ($22M)**, far exceeding others. Pedals, Tires, and Tubes also have **high spending ($13M each)**, while Jerseys, Shorts, Vests, and Bib-Shorts are **much lower ($1M or less)**.

→ Spending is **heavily concentrated in Pedals, Tires, and large unclassified "(Blank)" items**.

### 📈 II. Product Analysis

![Image](https://github.com/user-attachments/assets/da07a0f4-da91-4480-9d7d-a9b89e608562)

### 📌 Key Findings:

#### 1. Purchase Volume & Average Price
- Purchase volume peaked between **April–August**, then slightly declined in **October**.
- The **average purchase price** steadily rose from **34.1** to **35.5**, even as volume slowed.

#### 2. Inventory Turnover
- **Inventory turnover** peaked in **June–July** (23K), reflecting strong mid-year demand.
- From **September** onward, turnover dropped sharply, indicating slower stock movement.

#### 3. SKUs Below Thresholds
- Key SKUs are below safety stock levels, notably **HL Mountain Frame (145 SKUs)** and **ML Touring Frame (98 SKUs)**.
- This increases the risk of **stockouts** if demand rises or new orders come in.

#### 4. Product & Finished Goods Overview
- Finished goods ratio ranges from **33–47%**, showing imbalance across product groups.
- Low levels in some groups may affect **order fulfillment**.

#### 5. Total Spend by Product
- Spending is concentrated on frame lines: **HL Mountain Frame ($1.13M)** leads, followed by **ML Touring Frame ($1.01M)**.
- Other product lines have significantly lower spend.

#### 6. PO & Backorder Rate
- Total POs for **Components** are small, but the **backorder rate is highest (18%)**, suggesting potential vendor supply gaps.

#### 7. Inventory Status
- Many SKUs are **overstocked**. The system recommends **pausing purchasing** for these items to prevent inventory buildup.

### III. 🤝 Vendor Performance

![Image](https://github.com/user-attachments/assets/27a04562-6258-4915-bc6a-f7ce96745722)

### 📌 Key Findings:

#### 1. PO Cost Variance & Pareto Analysis
- **Superior Bicycles** accounts for **20.6%** of total PO cost variance, having a major impact on purchasing costs.
- The top 5 vendors contribute over **50%** of total variance, highlighting a high concentration that requires tighter cost control.

#### 2. Vendor Spend & Backorder Risk
- **Superior Bicycles** has the highest spend (**$4.56M**) but also a high backorder rate (**20%**).
- **Chicago City Saddles** has the **highest backorder (21.6%)**, indicating a significant fulfillment risk.
- Vendors like **Victory Bikes (11.8%)** and **Inline Accessories (9.8%)** show lower backorder rates, supporting more stable supply.

#### 3. Average PO Cost & Price Trend
- **Superior Bicycles** leads in **average PO cost ($45.5K)** with a rising price trend over the last 6 months.
- Other vendors, e.g., **Inline Accessories ($34.4K)**, maintain stable pricing, reducing exposure to cost volatility.

#### 4. Vendor Segmentation by Spend & Rating
- **Victory Bikes** and **Proseware, Inc.** show balanced spend and higher ratings, positioning them favorably.
- **Chicago City Saddles** and **Superior Bicycles**, despite high spend, carry higher fulfillment risks and need closer monitoring.

#### 5. Preferred Vendor Pipeline
- **91%** of the purchasing pipeline is allocated to **preferred vendors**, ensuring strategic alignment but requiring careful performance tracking.

# 🔎 Final Conclusion & Recommendation

| **Aspect**                     | **Insight**                                                                                                      | **Recommendation**                                                                                       |
|---------------------------------|------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| **Order & PO Performance**      | - **Demand peaks in May–June**, causing operational strain. **Late Orders** and **Back Order Rate** hit their highest in June–July (~10.5%). Performance improves steadily after August. | - Enhance **order handling during peak periods** to reduce pressure. <br> - Optimize **processing for at-risk orders**. |
| **PO Cost & Trends**            | - **PO costs fluctuate** seasonally, peaking in March and dropping sharply by October. Costs stabilize around **$7.0K–$7.2K** by year-end. | - Maintain **tight PO cost control**, especially toward year-end. <br> - **Monitor cost trends** and adjust procurement strategy to prevent sudden spikes. |
| **Vendor Performance & Risks**  | - Key suppliers like **Chicago City** and **Superior Bicycles** have **high costs** and significant **backorder risks** (**21.6% and 20%**), impacting delivery reliability. | - Consider **renegotiating prices** or alternative suppliers for high-cost vendors. <br> - Strengthen **delivery processes** or reassess suppliers if backorder rates remain high. |
| **Product & Inventory Management** | - **Incomplete product classification** hampers accurate spending tracking. The **Blank** category accounts for **$22M**, while items like **Jerseys** and **Vests** show low spend. | - Improve **product classification** to better track spending. <br> - Focus on **high-spending categories** like Pedals, Tires, and Tubes to optimize purchasing and resource allocation. |


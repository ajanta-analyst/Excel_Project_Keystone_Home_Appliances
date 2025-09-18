# Keystone Home Appliances — Sales Dashboard (Excel)

A single-page Excel dashboard for a retailer that compares **Selected Year vs Other Years**, highlights **Top Products**, **Channel Mix (Online vs In-Store)**, and **Revenue by State**, and is ready for weekly executive reviews.

---

## Dashboard
- **Dashboard (view/download):** _https://drive.google.com/file/d/1ZQLyQXW-sFxwCd3TEtSre_CJNm42ciEY/view?usp=drive_link_

![Image](https://github.com/user-attachments/assets/1aa84a67-dffc-420b-98d5-a183ef9b4693)


## Table of Contents
- [About the Project](#about-the-project)
- [Dataset (Synthetic)](#dataset-synthetic)
- [Business Questions](#business-questions)
- [Features & KPIs](#features--kpis)
- [Steps Followed](#steps-followed)
- [Contact](#contact)

---

##  About the Project
**Goal:** Give leaders a fast, clean snapshot of performance for the selected year, with clear levers by **Product**, **Channel**, and **Geography**.  
**Tech:** Microsoft Excel (tables, dynamic arrays, charts, map, form controls).  
**Brand:**  **Keystone Home Appliances**.(Dummy Data)

---

##  Dataset 
Columns:
- `Date`, `Year`, `Product`, `State`, `Channel (Online/In-Store)`, `Revenue`, `Qty Sold`.

> This dataset is  created for portfolio demonstration only.

---

##  Business Questions
1. What share of total revenue does the **selected year** contribute vs **other years**?  
2. Which **products** drive the most revenue?  
3. What is the **Online vs In-Store** mix?  
4. Which **states** contribute most to **Revenue** and **Qty Sold**?  
5. What actions should we take next (recommendations)?

---

##  Features & KPIs
- **Selected Year vs Others** KPI (donut %)
- **Top Products by Revenue** (sorted horizontal bars)
- **Channel Mix**: Online % vs In-Store %
- **US Map**: Revenue by State (with Qty toggle)
- **Revenue-to-date** card
- **Recommendations** panel (data-driven notes)

---

## Steps Followed
**1) Load & structure data**  
- Imported the table as an Excel **Table** (`tblSales`) with the columns above.
- Set up a small **Parameters** area for `selYear` and `selProduct`.

**2) Selectors (no Pivot needed)**  
- **Data Validation → List** for Year and Product pickers.
- Helper cells store current selections (`selYear`, `selProduct`).

**3) Core measures with `SUMIFS`**  
- Selected Year Revenue:  
  `=SUMIFS(tblSales[Revenue], tblSales[Year], selYear)`  
- Other Years Revenue:  
  `=SUMIFS(tblSales[Revenue], tblSales[Year], "<>" & selYear)`  
- Selected Year Qty:  
  `=SUMIFS(tblSales[Qty Sold], tblSales[Year], selYear)`

**4) Donut KPI**  
- Two-row table `{Selected; Others}` bound to measures → **Doughnut chart** with large % label.

**5) Top Products (SUMIFS + LARGE + INDEX/MATCH)**  

- **5A) Revenue per product (selected year)**

=SUMIFS(tblSales[Revenue], tblSales[Product], $A2, tblSales[Year], selYear) 

- **5B) Top-N values**

=LARGE($B$2:$B$200, E2)  

- **5C) Top-N product names**

=INDEX($A$2:$A$200, MATCH(F2, $B$2:$B$200, 0))

**6) Channel Mix**  
- Online & In-Store with `SUMIFS`; show bold **%** labels.

**7) Geography (US Map)**  
- State summary table for selected year (Revenue, Qty).  
- Insert → **Map** chart bound to the state table.

**8) Product navigation**  
- **Spin Button** (Developer → Form Controls) to scroll ranked products for live demos.

**9) Dynamic headers & narrative**  
- Title cell:  
  `="Summary for " & selProduct & " for the year " & selYear`  
- Recommendations fed by simple rule checks (e.g., channel share, top states).

**10) Formatting & layout**  
- Currency in K format (`$#,##0,"K"`).  
- Consistent palette, fixed chart sizes (**Don’t move or size with cells**).  
- Grouped elements for clean export.

**11) Export**  
- **File → Export → PDF** for weekly reviews.

---



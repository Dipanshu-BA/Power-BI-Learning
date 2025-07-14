# 📊 Power BI DAX Cheat Sheet

A comprehensive guide to essential **DAX (Data Analysis Expressions)** concepts, functions, and examples — perfect for beginners and intermediates working in **Power BI**.

---

## 📚 Table of Contents

- [🧠 Data Model Basics](#-data-model-basics)
- [🗃️ Fact & Dimension Tables](#️-fact--dimension-tables)
- [🔑 Keys & Relationships](#-keys--relationships)
- [⭐ Star vs Snowflake Schema](#-star-vs-snowflake-schema)
- [🔄 Relationships: Active, Inactive, Cardinality](#-relationships-active-inactive-cardinality)
- [🔀 Filter Context & Flow](#-filter-context--flow)
- [↔️ Bidirectional Filters & Ambiguity](#-bidirectional-filters--ambiguity)
- [➕ Basic Math & Stats Functions](#-basic-math--stats-functions)
- [📆 Time Intelligence Functions](#-time-intelligence-functions)
- [🧠 Conditional & Logical Functions](#-conditional--logical-functions)
- [✏️ Text Functions](#-text-functions)
- [📅 Date & Time Functions](#-date--time-functions)
- [🔗 Joining Tables with `RELATED`](#-joining-tables-with-related)
- [🧮 `CALCULATE` Function](#-calculate-function)
- [🚫 `ALL` Function](#-all-function)
- [🔍 `FILTER` Function](#-filter-function)
- [🔁 Iterator Functions (`SUMX`, `RANKX`, etc.)](#-iterator-functions-sumx-rankx-etc)

---

## 🧠 Data Model Basics
> A data model is the **foundation** of your Power BI report where **tables, relationships, and measures** are defined for analysis.

---

## 🗃️ Fact & Dimension Tables
- **Fact Table**: Contains **measurable data** (e.g., Sales).
- **Dimension Table**: Contains **descriptive attributes** (e.g., Product, Region).

---

## 🔑 Keys & Relationships
- **Primary Key**: Uniquely identifies a record (e.g., `CustomerID` in Customers).
- **Foreign Key**: Connects a fact table to a dimension table via a key.

---

## ⭐ Star vs Snowflake Schema
- **Star Schema**: Flat, denormalized — Fact table directly linked to dimension tables.
- **Snowflake Schema**: Normalized — Dimension tables split into sub-tables.

---

## 🔄 Relationships: Active, Inactive, Cardinality
- **Active Relationship**: Solid line in model, used by default.
- **Inactive Relationship**: Dotted line; needs `USERELATIONSHIP()` in DAX.
- **Cardinality**: Type of relation — One-to-many, many-to-one, etc.

---

## 🔀 Filter Context & Flow
- **Filter Context**: Filters applied by visuals, slicers, and measures.
- **Filter Flow**: Direction filters move between related tables.

---

## ↔️ Bidirectional Filters & Ambiguity
- **Bidirectional Filter**: Allows filter flow in both directions.
- **Ambiguity**: Occurs when multiple filter paths cause confusion.

---

## ➕ Basic Math & Stats Functions

| Function | Example |
|---------|---------|
| `SUM` | `= SUM(Sales[Amount])` |
| `AVERAGE` | `= AVERAGE(Sales[Amount])` |
| `COUNT` | `= COUNT(Sales[OrderID])` |
| `DISTINCTCOUNT` | `= DISTINCTCOUNT(Sales[CustomerID])` |
| `ROUND` | `= ROUND(Price, 2)` |

---

## 📆 Time Intelligence Functions


Sales YTD = TOTALYTD([Total Sales], 'Date'[Date])
Sales MTD = TOTALMTD([Total Sales], 'Date'[Date])
Sales Last Year = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date]))


## 🧠 Conditional & Logical Functions

```dax
IF(Sales[Amount] > 1000, "High", "Low")

SWITCH(TRUE(),
    [Sales] > 10000, "High",
    [Sales] > 5000, "Medium",
    "Low"
)

IF(AND([Profit] > 0, [Sales] > 1000), "Good", "Bad")

```

## ✏️ Text Functions
```dax
= CONCATENATE(FirstName, LastName)
= LEFT(ProductCode, 3)
= RIGHT(EmployeeID, 4)
= MID(Code, 2, 3)
= FORMAT(Date, "MMM-YYYY")
= TRIM(Name)
```

## 📅 Date & Time Functions
```dax
TODAY() — returns current date  
YEAR(OrderDate) — returns year  
DATEDIFF(StartDate, EndDate, DAY)  
EOMONTH(Date, -1) — end of last month  
```

## 🔗 Joining Tables with RELATED
```
ProductName = RELATED(Products[ProductName])
Revenue = Sales[Qty] * RELATED(Products[Price])
```

## 🧮 CALCULATE Function
```
High Sales = CALCULATE(SUM(Sales[Amount]), Sales[Amount] > 1000)
Sales for North = CALCULATE([Total Sales], Region[RegionName] = "North")
```

## 🚫 ALL Function
```
Total Sales All = CALCULATE(SUM(Sales[Amount]), ALL(Sales))
% of Total = DIVIDE([Total Sales], CALCULATE([Total Sales], ALL(Products)))
```

## 🔍 FILTER Function
```
High Value Orders = 
CALCULATE(
    [Total Sales],
    FILTER(Sales, Sales[Amount] > 1000)
)
```

## 🔁 Iterator Functions (SUMX, RANKX, etc.)
```
Total Revenue = SUMX(Sales, Sales[Quantity] * Sales[UnitPrice])
Product Rank = RANKX(ALL(Products), [Total Sales], , DESC)
Average Order = AVERAGEX(Sales, Sales[Amount])
```



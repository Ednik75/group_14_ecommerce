# CS27 — E-Commerce Platform Database
### End-of-Semester Group Project
**Burkina Institute of Technology — Computer Science Department**
**Course:** CS27 – The Relational Model & Databases
**Instructor:** Kweyakie Afi Blebo | blebo.kweyakie@bit.bf

---

## 👥 Group Members

| # | Full Name | Role |
|---|---|---|
| 1 | NITIEMA Teegawendé Eddy Martial | Introduction & Scenario Overview |
| 2 | YANOGO Fabiana Stéphanie | Entity Design & Relationships |
| 3 | OUEDRAOGO Akram Mu'min | Normalization Walkthrough |
| 4 | DAH Nibouor Chèoutièrou | Live MySQL Demo: CREATE & INSERT |
| 5 | KIENDREBEOGO Moussa | Live MySQL Demo: SELECT Queries |
| 6 | KABORE Oceanne | Aggregate Queries & Conclusion |

---

## 📋 Scenario
**Scenario 3 — E-Commerce Platform**

A fully normalized relational database modelling a real-world online store.
The system handles customer accounts, product catalogues, order management, and payment processing.

---

## 🗄️ Database: EcommerceBIT_EN

### Tables (6 total — normalized to 3NF)

| Table | Description | Key Constraint |
|---|---|---|
| `Customers` | Customer personal information | UNIQUE on email |
| `Categories` | Product categories | UNIQUE on category_name |
| `Products` | Product catalogue with prices and stock | FK → Categories (ON DELETE SET NULL) |
| `Orders` | Customer purchase records | FK → Customers (ON DELETE CASCADE) |
| `Order_Items` | Junction table — resolves M:N between Orders and Products | FK → Orders + Products |
| `Payments` | Payment records per order | UNIQUE on order_id (1:1 with Orders) |

### Relationships

| Relationship | Type | Description |
|---|---|---|
| Customers → Orders | 1 : M | One customer can place many orders |
| Categories → Products | 1 : M | One category contains many products |
| Orders ↔ Products | M : N | Resolved via Order_Items junction table |
| Orders → Order_Items | 1 : M | One order has many line items |
| Orders → Payments | 1 : 1 | One order has exactly one payment |

---

## 📁 Repository Structure

```
cs27-ecommerce/
├── Projet (1).sql              # Main SQL file — Parts 2 & 3
├── part1_design_document.docx  # Part 1 — Database Design document
├── part5_script_FINAL.docx     # Part 5 — Video Walkthrough Script
└── README.md                   # This file
```

---

## 🚀 How to Run

### Requirements
- MySQL 8.0+ or MariaDB 10.4+
- phpMyAdmin or MySQL Workbench

### Steps

**1.** Open phpMyAdmin in your browser:
```
http://localhost/phpmyadmin
```

**2.** Click **Import** in the top menu (without selecting any database first)

**3.** Select the file **`Projet (1).sql`** → click **Execute**

**4.** The database `EcommerceBIT_EN` will be created automatically with all 6 tables and sample data

**5.** Click on **EcommerceBIT_EN** in the left panel to start querying

---

## 📊 Sample Data

| Table | Rows | Details |
|---|---|---|
| Customers | 10 | Burkinabè names and cities |
| Categories | 10 | Electronics, Fashion, Books, etc. |
| Products | 10 | Prices in FCFA |
| Orders | 10 | Statuses: Pending, Shipped, Delivered, Cancelled |
| Order_Items | 10 | Quantities and unit prices |
| Payments | 10 | Methods: Orange Money, Moov Money, Credit Card, Cash, PayPal |

---

## 🔍 SQL Features Demonstrated

### Part 2 — MySQL Implementation

| Feature | Example |
|---|---|
| CREATE TABLE | PRIMARY KEY, FOREIGN KEY, NOT NULL, UNIQUE, DEFAULT, CHECK |
| INSERT | 10+ realistic rows per table |
| UPDATE | 3 statements — price, status, address |
| DELETE | 2 statements — order item, payment |
| FK Violation | `DELETE FROM Products WHERE product_id = 1` → ERROR 1451 |
| SELECT * | All records from a table |
| WHERE | Filter by specific condition |
| ORDER BY | Sort results ascending / descending |
| LIMIT | Restrict number of results |
| BETWEEN | Filter by price range |
| LIKE | Pattern matching on product names |
| IN | Filter by list of values |
| INNER JOIN | Orders with customer names |
| LEFT JOIN | All customers including those with no orders |
| 4-table JOIN | Customer → Order → Order_Items → Product |
| IS NULL / IS NOT NULL | Products with or without a category |

### Part 3 — Aggregate Functions & Reporting

| Function | Description |
|---|---|
| COUNT | Total number of customers |
| MAX / MIN | Highest and lowest product price |
| AVG | Average product price |
| SUM | Total revenue from all payments |
| GROUP BY | Revenue grouped by payment method |
| HAVING | Payment methods generating more than 100,000 FCFA |
| Complex Report | Top spending customers — JOIN + GROUP BY + HAVING + ORDER BY |

---

## 📐 Normalization Summary

| Step | Problem | Fix Applied |
|---|---|---|
| **UNF → 1NF** | Repeating columns: product_id_1, product_id_2... | One row per (order, product) pair |
| **1NF → 2NF** | Partial dependencies on customer_id and product_id | Extracted Customers and Products tables |
| **2NF → 3NF** | Transitive dependencies: category_name in Products, payment fields in Orders | Extracted Categories and Payments tables |

**Final result:** 6 tables in Third Normal Form (3NF).

---

## 🎥 Video Walkthrough

📺 YouTube: *[Insert your YouTube link here]*
⏱️ Duration: 7–9 minutes
👥 All 6 members participate

**Video covers:**
- Scenario overview and entity design
- Normalization walkthrough (UNF → 3NF)
- Live MySQL demo in phpMyAdmin
- SELECT queries including JOINs
- Aggregate functions and final report



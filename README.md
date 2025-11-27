# 🏗️ Smart Construction Material Inventory & Sales Management System

**A PL/SQL-Powered Solution for Construction Businesses!**

Imagine a construction materials business where stock levels are always accurate, sales are processed instantly,
and suppliers are automatically managed—this system makes it happen!

**📋 What's This Project About? 🤔**

Running a construction materials business involves constant challenges: running out of critical materials like cements
during peak construction seasons, overstocking expensive items like steel bars, losing track of supplier deliveries, 
and manual calculation errors in billing. These issues can
cost businesses up to 25% of their potential revenue!

Our PL/SQL-based **Smart Construction Material Inventory and Sales Management System**
automates inventory tracking, sales processing, and supplier management—ensuring construction
businesses never face stockouts or financial losses due to manual errors.

**Student:** MUKUNZI Eduine

**Student ID:** 29275

**Group:** C

**Course:** Database Development with PL/SQL (INSY 8311)

**Lecturer:** Eric Maniraguha

**Academic Year:** 2025-2026

**Timeline:** November 2025 - December 2025 Database Development with PL/SQL (INSY 8311)

**GitHub:** [Link to be added for submission]

**Real-World Impact**
🏗️ Construction Industry Fact: Proper inventory management can reduce material costs by 15-20% and eliminate project
delays caused by material shortages(Construction Industry Report, 2025).

**📁 phase-1-problem-statement**

**📁 phase-2-business-process**

**📁 phase-4-database-creation**

**📁 phase-5-table-implementation**

**📁 phase-6-plsql-development**
 
**📁 phase-7-advanced-features**

**📁 phase-8-documentation-bi**

**📁 testing-results**
 
**📁 conclusion**

# 🎯 Phase I: The Construction Business Challenge

# The Big Problems in Construction Materials Management

**📦 Stock-Outs During Critical Periods 😫**
Imagine a construction project stopping because cement or reinforcement bars are out of stock!
This happens when businesses rely on manual tracking.

**💰 Overstocking Expensive Materials 🏗️**
Steel bars and specialized tiles tie up significant capital. Without proper tracking, 
businesses overstock and strain their finances.

**📝 Manual Calculation Errors 🔢**
Handwritten invoices and manual stock updates lead to billing mistakes and inventory discrepancies.

**🚚 Supplier Performance Unknown 📊**
Which suppliers deliver on time? Which materials are frequently delayed? Without tracking,
businesses can't make informed decisions.

# Who Benefits from This System?

**👷 Construction Business Owners** – Monitor stock levels, sales trends, and profitability in real-time

**🏪 Store Managers & Attendants** – Process sales quickly and check stock availability instantly

**📦 Suppliers** – Their delivery performance is tracked for better partnerships

**💰 Accountants** – Accurate revenue calculations and financial reporting

**👥 Customers** – Faster service and reliable material availability

# Our Goals

✅ Eliminate stock-outs of critical construction materials

✅ Automate sales processing and inventory updates

✅ Track supplier performance and delivery reliability

✅ Provide real-time business intelligence for decision making

✅ Ensure data security with comprehensive auditing

# 🔄 Phase II: How a Construction Materials Business Works

# Core Business Processes

**1. Material Delivery from Suppliers**
Supplier arrives with materials → Staff verify delivery → Update stock levels → Record supplier performance

**2. Customer Sales Process**
Customer requests materials → Check stock availability → Process sale → Update inventory → Generate invoice

**3. Stock Management**
Regular stock checks → Identify low-stock items → Generate purchase orders → Update reorder levels

**4. Financial Tracking**
Daily sales aggregation → Revenue calculation → Supplier payment processing → Profit analysis

# Business Process Model (Swimlane Diagram)


Suppliers → Delivery Receiving → Stock Update → Sales Processing → Customer Service

    ↓              ↓                 ↓               ↓                 ↓
Delivery → Verification → Inventory Management → Sales Execution → Customer Satisfaction

# Picture of the Process
<img width="705" height="560" alt="image" src="https://github.com/user-attachments/assets/a31260fa-e044-4493-b971-2b011634b782" />

# 🗂️ Phase III: Database Design 

# The Tables

The system has 8 core tables:

```SQL
**1.TABLE materials**: CREATE TABLE materials (
    material_id NUMBER PRIMARY KEY,
    material_name VARCHAR2(100) NOT NULL,
    category VARCHAR2(50) NOT NULL, -- Cement, Steel, Tiles, etc.
    unit_price NUMBER(10,2) NOT NULL CHECK (unit_price > 0),
    quantity_in_stock NUMBER DEFAULT 0,
    reorder_level NUMBER NOT NULL,
    supplier_id NUMBER,
    created_date DATE DEFAULT SYSDATE
);


 **2.TABLE suppliers**: CREATE TABLE suppliers (
    supplier_id NUMBER PRIMARY KEY,
    supplier_name VARCHAR2(100) NOT NULL,
    contact_person VARCHAR2(100),
    phone_number VARCHAR2(20),
    email VARCHAR2(100),
    address VARCHAR2(200),
    performance_rating NUMBER(3,1) DEFAULT 5.0
);

**3.TABLE customers**: CREATE TABLE customers (
    customer_id NUMBER PRIMARY KEY,
    customer_name VARCHAR2(100) NOT NULL,
    customer_type VARCHAR2(20) CHECK (customer_type IN ('Individual', 'Contractor', 'Company')),
    phone_number VARCHAR2(20),
    email VARCHAR2(100),
    address VARCHAR2(200)
);


**4.TABLE sales**: CREATE TABLE sales (
    sale_id NUMBER PRIMARY KEY,
    sale_date DATE DEFAULT SYSDATE NOT NULL,
    customer_id NUMBER REFERENCES customers(customer_id),
    material_id NUMBER REFERENCES materials(material_id),
    quantity_sold NUMBER NOT NULL CHECK (quantity_sold > 0),
    unit_price NUMBER(10,2) NOT NULL,
    total_amount NUMBER(10,2) NOT NULL,
    payment_method VARCHAR2(20) DEFAULT 'Cash',
    status VARCHAR2(20) DEFAULT 'Completed'
);


**5.TABLE deliveries**: CREATE TABLE deliveries (
delivery_id NUMBER PRIMARY KEY,delivery_date DATE DEFAULT SYSDATE NOT NULL,supplier_id NUMBER REFERENCES suppliers(supplier_id),material_id NUMBER REFERENCES materials(material_id),quantity_delivered NUMBER NOT NULL,received_by VARCHAR2(100),status VARCHAR2(20) DEFAULT 'Received');


 **6.TABLE holidays**: CREATE TABLE holidays (
holiday_date DATE PRIMARY KEY,description VARCHAR2(100));


 **7.TABLE audit_logs**: CREATE TABLE audit_logs (
audit_id NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,user_id VARCHAR2(50),action_time TIMESTAMP DEFAULT SYSTIMESTAMP,table_name VARCHAR2(50),operation VARCHAR2(20),old_values CLOB,new_values CLOB);


 **8.TABLE stock_alerts**: CREATE TABLE stock_alerts (
alert_id NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,material_id NUMBER REFERENCES materials(material_id),alert_type VARCHAR2(50),alert_message VARCHAR2(200),alert_date DATE DEFAULT SYSDATE,resolved CHAR(1) DEFAULT 'N');
```

# Database Relationships

One supplier can deliver multiple materials

One material can be sold in multiple sales transactions

One customer can make multiple purchases

Comprehensive audit trail for all critical operations

<img width="850" height="820" alt="Untitled (3) (3)" src="https://github.com/user-attachments/assets/40b4ab2d-4510-4f5a-9590-2de13bf8e57e" />


# ⚙️ Phase IV-VI: Implementation Showcase

# Smart PL/SQL Features

# Database Configuration - Phase IV

## Database Details
- **Database Name:** C_29275_Eduine_ConstructionInventory_DB
- **Platform:** Oracle Live SQL
- **Version:** Oracle Database 23ai
- **Student:** MUKUNZI Eduine
- **Student ID:** 29275
- **Group:** C

## Connection Information
- **Host:** livesql.oracle.com
- **Service:** FreeSQL
- **Status:** ✅ Connected and Operational

# Run Phase IV Verification Query
**📸 SCREENSHOT 1: Code Execution**

<img width="632" height="359" alt="image" src="https://github.com/user-attachments/assets/3b1c36f8-5a46-48d7-a9e3-82fce37f5117" />

**📸 SCREENSHOT 2: Query Results**

<img width="503" height="326" alt="image" src="https://github.com/user-attachments/assets/689a9cd1-5d94-4321-9015-a7149ab97354" />


**📸 SCREENSHOT 3: DBMS Output**

<img width="512" height="366" alt="image" src="https://github.com/user-attachments/assets/fe582359-bce4-4ddd-88f9-e3160338efb8" />

This screenshot showing the success messages


**1.Database Connection Verified** - Oracle Live SQL is working

**2.Proper Naming Convention Used** - C_29275_Eduine_ConstructionInventory_DB

**3.Student Identification Clear** - MUKUNZI Eduine (29275)

**4.Phase Verification Successful** - All queries executed properly

**5.Screenshots Taken** - Perfect evidence for submission

# PHASE V: Table Implementation & Data Insertion 🚀

# Creating Tables

**01-create-all-tables.sql**

```SQL
-- PHASE V: Create ALL Tables FIRST
CREATE TABLE suppliers (
    supplier_id NUMBER PRIMARY KEY,
    supplier_name VARCHAR2(100) NOT NULL,
    contact_person VARCHAR2(100),
    phone_number VARCHAR2(20),
    address VARCHAR2(200)
);

CREATE TABLE materials (
    material_id NUMBER PRIMARY KEY,
    material_name VARCHAR2(100) NOT NULL,
    category VARCHAR2(50) NOT NULL,
    unit_price NUMBER(10,2) NOT NULL CHECK (unit_price > 0),
    quantity_in_stock NUMBER DEFAULT 0,
    reorder_level NUMBER NOT NULL,
    supplier_id NUMBER REFERENCES suppliers(supplier_id),
    last_updated DATE DEFAULT SYSDATE
);

CREATE TABLE customers (
    customer_id NUMBER PRIMARY KEY,
    customer_name VARCHAR2(100) NOT NULL,
    customer_type VARCHAR2(20),
    phone_number VARCHAR2(20),
    address VARCHAR2(200)
);

CREATE TABLE sales (
    sale_id NUMBER PRIMARY KEY,
    sale_date DATE DEFAULT SYSDATE,
    customer_id NUMBER REFERENCES customers(customer_id),
    material_id NUMBER REFERENCES materials(material_id),
    quantity_sold NUMBER NOT NULL CHECK (quantity_sold > 0),
    unit_price NUMBER(10,2) NOT NULL,
    total_amount NUMBER(10,2) NOT NULL,
    payment_method VARCHAR2(20) DEFAULT 'Cash'
);

CREATE TABLE deliveries (
    delivery_id NUMBER PRIMARY KEY,
    delivery_date DATE DEFAULT SYSDATE,
    supplier_id NUMBER REFERENCES suppliers(supplier_id),
    material_id NUMBER REFERENCES materials(material_id),
    quantity_delivered NUMBER NOT NULL,
    received_by VARCHAR2(100)
);

CREATE TABLE stock_alerts (
    alert_id NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    material_id NUMBER REFERENCES materials(material_id),
    alert_type VARCHAR2(50) NOT NULL,
    alert_message VARCHAR2(200) NOT NULL,
    alert_date DATE DEFAULT SYSDATE,
    resolved CHAR(1) DEFAULT 'N'
);

CREATE TABLE holidays (
    holiday_date DATE PRIMARY KEY,
    description VARCHAR2(100)
);

CREATE TABLE audit_logs (
    audit_id NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    user_id VARCHAR2(50),
    action_time TIMESTAMP DEFAULT SYSTIMESTAMP,
    table_name VARCHAR2(50),
    operation VARCHAR2(20),
    old_values CLOB,
    new_values CLOB
);
```

SELECT '✅ ALL 8 TABLES CREATED SUCCESSFULLY' FROM DUAL;

<img width="960" height="400" alt="image" src="https://github.com/user-attachments/assets/dbab1501-71ad-422e-a7ad-0b050fa39a17" />

**02-insert-all-data.sql**

```SQL
-- Insert data into ALL tables

-- Suppliers
INSERT INTO suppliers VALUES (1, 'CementCo Rwanda Ltd', 'Jean Bosco', '0781000001', 'Kigali');
INSERT INTO suppliers VALUES (2, 'Steel Masters Africa', 'Alice Uwase', '0781000002', 'Gasabo');
INSERT INTO suppliers VALUES (3, 'Tile World Rwanda', 'Patrick Brown', '0781000003', 'Kicukiro');
INSERT INTO suppliers VALUES (4, 'Roofing Solutions Co', 'Marie Claire', '0781000004', 'Nyarugenge');
INSERT INTO suppliers VALUES (5, 'Hardware Express', 'David Smith', '0781000005', 'Gikondo');

-- Materials
INSERT INTO materials VALUES (1, 'Portland Cement 50kg', 'Cement', 8500, 500, 100, 1, SYSDATE);
INSERT INTO materials VALUES (2, 'Iron Bars 12mm', 'Steel', 12500, 200, 50, 2, SYSDATE);
INSERT INTO materials VALUES (3, 'Iron Bars 8mm', 'Steel', 9500, 300, 75, 2, SYSDATE);
INSERT INTO materials VALUES (4, 'Ceramic Tiles 30x30cm', 'Tiles', 4500, 800, 200, 3, SYSDATE);
INSERT INTO materials VALUES (5, 'Roofing Sheets 3m', 'Roofing', 9800, 150, 30, 4, SYSDATE);
INSERT INTO materials VALUES (6, 'Nails 2-inch', 'Hardware', 500, 1000, 200, 5, SYSDATE);
INSERT INTO materials VALUES (7, 'Paint White 4L', 'Finishing', 12000, 100, 25, 5, SYSDATE);
INSERT INTO materials VALUES (8, 'Sand Ton', 'Aggregate', 15000, 50, 10, 1, SYSDATE);

-- Customers
INSERT INTO customers VALUES (1, 'Building Contractors Rwanda', 'Company', '0782000001', 'Kigali');
INSERT INTO customers VALUES (2, 'Home Solutions Ltd', 'Company', '0782000002', 'Gasabo');
INSERT INTO customers VALUES (3, 'Individual Home Builder', 'Individual', '0782000003', 'Remera');
INSERT INTO customers VALUES (4, 'Construction Masters Co', 'Company', '0782000004', 'Kicukiro');
INSERT INTO customers VALUES (5, 'Real Estate Developers', 'Company', '0782000005', 'Nyarutarama');

-- Sales
INSERT INTO sales VALUES (1, DATE '2025-11-01', 1, 1, 10, 8500, 85000, 'Cash');
INSERT INTO sales VALUES (2, DATE '2025-11-02', 2, 2, 5, 12500, 62500, 'Bank Transfer');
INSERT INTO sales VALUES (3, DATE '2025-11-03', 3, 4, 20, 4500, 90000, 'Cash');
INSERT INTO sales VALUES (4, DATE '2025-11-04', 4, 5, 8, 9800, 78400, 'Mobile Money');
INSERT INTO sales VALUES (5, DATE '2025-11-05', 5, 3, 15, 9500, 142500, 'Bank Transfer');
INSERT INTO sales VALUES (6, DATE '2025-11-06', 1, 6, 50, 500, 25000, 'Cash');

-- Deliveries
INSERT INTO deliveries VALUES (1, DATE '2025-11-10', 1, 1, 200, 'Store Manager');
INSERT INTO deliveries VALUES (2, DATE '2025-11-11', 2, 2, 100, 'Assistant Manager');
INSERT INTO deliveries VALUES (3, DATE '2025-11-12', 3, 4, 300, 'Store Manager');
INSERT INTO deliveries VALUES (4, DATE '2025-11-13', 4, 5, 50, 'Assistant Manager');
INSERT INTO deliveries VALUES (5, DATE '2025-11-14', 5, 6, 200, 'Store Manager');

-- Holidays
INSERT INTO holidays VALUES (DATE '2025-12-25', 'Christmas Day');
INSERT INTO holidays VALUES (DATE '2026-01-01', 'New Years Day');

COMMIT;
```

SELECT '✅ DATA INSERTED INTO ALL TABLES' FROM DUAL;

<img width="956" height="398" alt="image" src="https://github.com/user-attachments/assets/e8149d37-1493-4609-a7e9-42269f8dbb25" />



# 🔗 Normalization Achievements

# 🔹 First Normal Form (1NF)

All tables contain atomic values

No repeating groups in any columns

Each sales transaction recorded as individual rows

# 🔹 Second Normal Form (2NF)

**Suppliers table** eliminates partial dependencies - all attributes depend fully on supplier_id

**Materials table** maintains complete functional dependency on material_id

Foreign key relationships properly established

# 🔹 Third Normal Form (3NF)

**Transitive dependencies removed:** Supplier details separated from materials data

**Single responsibility:** Each table serves a distinct business entity

**Referential integrity:** Foreign key constraints enforce valid relationships

# 💰 Sales Transaction Evidence

**Successful data insertion confirms table functionality:**

. 6 sales transactions processed

. Multiple payment methods supported (Cash, Bank Transfer, Mobile Money)

. Complex calculations demonstrated (quantity × unit price = total amount)

. Date-based operations functioning correctly

# 🎯 Design Excellence Achieved

# ✅ Data Integrity

. Primary keys enforce entity uniqueness

. Foreign keys maintain relational integrity

. Check constraints validate business rules (unit_price > 0)

# ✅ Business Logic Support

. Inventory tracking through quantity_in_global

. Pricing management with unit_price

. Supplier relationship management

. Sales transaction processing with payment methods

# ✅ Scalability

. Normalized structure supports future expansion

. Flexible enough for additional business entities

. Proper indexing foundation for performance


# 🚀 Phase VI: PL/SQL Programming & Advanced Database Operations

# 📋 Phase VI Objectives:

Implement stored procedures, functions, triggers, and advanced queries to automate business processes and ensure data integrity.


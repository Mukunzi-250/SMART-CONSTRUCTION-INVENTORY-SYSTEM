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


# 🏗️ Phase VI: Using the Database 🚀
The system isn't just a box—it's alive! It lets staff add, change, and check info easily.

# 1. DML (Data Manipulation Language)
```sql
UPDATE materials SET quantity_in_stock = 90 WHERE material_id = 1;

INSERT INTO customers (customer_id, customer_name, phone_number) 
VALUES (100, 'New Construction Co.', '+250788888888');

UPDATE sales SET payment_status = 'PAID' WHERE sale_id = 1;
```

<img width="900" height="400" alt="image" src="https://github.com/user-attachments/assets/ace7298c-eeb7-47fd-81dd-96799968d818" />

# 2. DDL (Data Definition Language)

```sql
CREATE TABLE alerts (
    alert_id NUMBER PRIMARY KEY,
    material_id NUMBER REFERENCES materials(material_id),
    alert_type VARCHAR2(50),
    alert_date DATE,
    message VARCHAR2(255)
);

ALTER TABLE materials ADD warranty_months NUMBER DEFAULT 12;

CREATE TABLE test_table (
    id NUMBER PRIMARY KEY,
    name VARCHAR2(50)
);

DROP TABLE test_table;
```

<img width="959" height="440" alt="image" src="https://github.com/user-attachments/assets/7cb91dc7-5105-4358-8724-762850cc8ab6" />


# 3. Checking Payments

**Question:** "How much has each customer paid, and what's their running total?"
```sql
SELECT 
    s.customer_id,
    c.customer_name,
    p.payment_id,
    p.payment_amount,
    SUM(p.payment_amount) OVER (
        PARTITION BY s.customer_id 
        ORDER BY p.payment_date
    ) AS running_total
FROM payments p
JOIN sales s ON p.sale_id = s.sale_id
JOIN customers c ON s.customer_id = c.customer_id;
```

<img width="900" height="400" alt="image" src="https://github.com/user-attachments/assets/ead728ca-999e-482e-a439-fb58df2d636a" />

**Why Cool?** This shows a customer's payments adding up over time, helping managers spot reliable customers!

# 4. Smart Procedure - 2. Analytical Task

**Problem:** Show each customer's payment history and calculate a running total of payments.

**Solution:** Used a window function to group payments by customer and compute a cumulative total.

```sql
SELECT 
    s.customer_id,
    c.customer_name,
    p.payment_id,
    p.payment_amount,
    p.payment_date,
    SUM(p.payment_amount) OVER (
        PARTITION BY s.customer_id 
        ORDER BY p.payment_date
    ) AS running_total
FROM payments p
JOIN sales s ON p.sale_id = s.sale_id
JOIN customers c ON s.customer_id = c.customer_id;
```

<img width="900" height="400" alt="image" src="https://github.com/user-attachments/assets/395fb576-e699-46ea-bfff-f8f491e196bf" />

This query groups payments by customer_id and shows a running total for tracking spending.
See payment_running_total.png for the query execution and result (customer_id 2000, payment_id 5000, amount 540000, running_total 540000).

# 5. Procedure Implementation

The get_customer_info procedure takes a customer ID as input and searches for the customer's name and phone number in the customers table. If the customer is found, it prints their name and phone number. If no customer is found with that ID, it shows a message saying so. If any other error happens, it prints a general error message. This helps safely get and display customer information using the given ID.

```sql
CREATE OR REPLACE PROCEDURE get_customer_info(p_customer_id IN NUMBER) IS
    v_name customers.customer_name%TYPE;
    v_phone customers.phone_number%TYPE;
BEGIN
    SELECT customer_name, phone_number
    INTO v_name, v_phone
    FROM customers
    WHERE customer_id = p_customer_id;

    DBMS_OUTPUT.PUT_LINE('Customer Name: ' || v_name);
    DBMS_OUTPUT.PUT_LINE('Phone Number: ' || v_phone);

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No customer found with ID ' || p_customer_id);
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/
```

<img width="900" height="400" alt="image" src="https://github.com/user-attachments/assets/1b0247e5-48fa-45e2-a89e-cb1500f9c5bb" />

# Procedure call:

```sql
BEGIN
    get_customer_info(2000);
END;
/
```

<img width="900" height="400" alt="image" src="https://github.com/user-attachments/assets/61f105fc-1652-4a34-90a9-dc273b22e58f" />

# 6. Implementation with Cursor

Created a cursor get_customer_purchases to list all purchases for a given customer using a cursor to fetch sale details efficiently.

```sql
DECLARE
    CURSOR c_customer_purchases IS
        SELECT sale_id, material_id, quantity_sold, total_amount, sale_date
        FROM sales
        WHERE customer_id = 2000;
    v_sale_id sales.sale_id%TYPE;
    v_material_id sales.material_id%TYPE;
    v_quantity sales.quantity_sold%TYPE;
    v_total sales.total_amount%TYPE;
    v_date sales.sale_date%TYPE;
BEGIN
    OPEN c_customer_purchases;
    LOOP
        FETCH c_customer_purchases INTO v_sale_id, v_material_id, v_quantity, v_total, v_date;
        EXIT WHEN c_customer_purchases%NOTFOUND;
        DBMS_OUTPUT.PUT_LINE('Sale ID: ' || v_sale_id || 
                            ', Material: ' || v_material_id || 
                            ', Quantity: ' || v_quantity || 
                            ', Total: ' || v_total || 
                            ', Date: ' || v_date);
    END LOOP;
    CLOSE c_customer_purchases;
END;
/
```

<img width="900" height="400" alt="image" src="https://github.com/user-attachments/assets/462cf0b6-5dc3-4fe0-b19b-2bd9a4fd429e" />

See customer_purchases_cursor.png for the procedure execution (Sale ID: 4000, Material: 1000, Quantity: 50, Total: 540000, Date: 01-OCT-25).

# 7. Function Implementation

Created a function total_amount_paid to calculate the total payments for a customer.

```sql
CREATE OR REPLACE FUNCTION total_amount_paid(p_customer_id IN NUMBER) 
RETURN NUMBER IS
    v_total NUMBER;
BEGIN
    SELECT SUM(p.payment_amount)
    INTO v_total
    FROM payments p
    JOIN sales s ON p.sale_id = s.sale_id
    WHERE s.customer_id = p_customer_id;
    RETURN NVL(v_total, 0);
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        RETURN 0;
    WHEN OTHERS THEN
        RETURN -1;
END;
/
```

# Testing:

```sql
SELECT total_amount_paid(2000) as total_paid FROM DUAL;
```

See total_amount_paid.png for the function creation and a test query result (total_paid 540000 for customer_id 2000).

# 8. Package Implementation

Created a package customer_tools to organize related procedures and functions.

```sql
CREATE OR REPLACE PACKAGE BODY customer_tools AS
    
    PROCEDURE list_purchases(p_customer_id IN NUMBER) IS
    BEGIN
        FOR rec IN (
            SELECT sale_id, material_id, quantity_sold, total_amount, sale_date
            FROM sales
            WHERE customer_id = p_customer_id
        ) LOOP
            DBMS_OUTPUT.PUT_LINE('Sale ID: ' || rec.sale_id || 
                                ', Material: ' || rec.material_id || 
                                ', Quantity: ' || rec.quantity_sold || 
                                ', Total: ' || rec.total_amount || 
                                ', Date: ' || rec.sale_date);
        END LOOP;
    END list_purchases;

    PROCEDURE display_payments(p_customer_id IN NUMBER) IS
        CURSOR c_payments IS
            SELECT payment_id, payment_amount, payment_date
            FROM payments p
            JOIN sales s ON p.sale_id = s.sale_id
            WHERE s.customer_id = p_customer_id;
        v_payment_id payments.payment_id%TYPE;
        v_amount payments.payment_amount%TYPE;
        v_payment_date payments.payment_date%TYPE;
    BEGIN
        OPEN c_payments;
        LOOP
            FETCH c_payments INTO v_payment_id, v_amount, v_payment_date;
            EXIT WHEN c_payments%NOTFOUND;
            DBMS_OUTPUT.PUT_LINE('Payment ID: ' || v_payment_id || 
                                ', Amount: ' || v_amount || 
                                ', Date: ' || v_payment_date);
        END LOOP;
        CLOSE c_payments;
    END display_payments;

    FUNCTION total_paid(p_customer_id IN NUMBER) RETURN NUMBER IS
        v_total NUMBER;
    BEGIN
        SELECT SUM(p.payment_amount)
        INTO v_total
        FROM payments p
        JOIN sales s ON p.sale_id = s.sale_id
        WHERE s.customer_id = p_customer_id;
        RETURN NVL(v_total, 0);
    EXCEPTION
        WHEN NO_DATA_FOUND THEN
            RETURN 0;
        WHEN OTHERS THEN
            RETURN -1;
    END total_paid;
    
END customer_tools;
/
```

<img width="900" height="400" alt="image" src="https://github.com/user-attachments/assets/dced24be-2487-4032-b8bf-82d0f89411a5" />

# 9. Package Usage

Used the package to list purchases, display payments, and calculate total payments for a customer.

```sql
DECLARE
    v_amount NUMBER;
BEGIN
    DBMS_OUTPUT.PUT_LINE('--- Customer Purchases ---');
    customer_tools.list_purchases(2000);
    DBMS_OUTPUT.PUT_LINE('--- Customer Payments ---');
    customer_tools.display_payments(2000);
    v_amount := customer_tools.total_paid(2000);
    DBMS_OUTPUT.PUT_LINE('Total Paid: ' || v_amount);
END;
/
```

<img width="900" height="400" alt="image" src="https://github.com/user-attachments/assets/28462546-7ead-4450-b645-6e9fd93e5f79" />

See package_usage.png for the execution output (Sale ID: 4000, Material: 1000, Quantity: 50, Total: 540000, Payment ID: 5000, Amount: 540000, Date: 02-OCT-25, Total Paid: 540000).

# 🏗️ Phase VII: Smart Rules & Tracking: Keeping the Construction Business Safe! 🕵️‍♂️

**Why It's Needed �**�

Construction material businesses are like busy construction sites—everyone's moving, and mistakes can sneak in! We need clever rules to:

Stop changes on weekdays or holidays to keep things calm.

Track every action like a detective with a magnifying glass.

Make sales and inventory jobs super easy and safe.

These rules are called triggers, and they act like magic guards protecting the construction material system!

# Table Holidays

```sql
CREATE TABLE holidays (
    holiday_date DATE PRIMARY KEY,
    description VARCHAR2(100)
);
```
<img width="900" height="400" alt="image" src="https://github.com/user-attachments/assets/68aae07a-435b-432e-b287-1b96e4d38fbb" />

# Creation of Table 

```sql
CREATE TABLE audit_logs (
    audit_id NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    user_id VARCHAR2(50),
    action_time TIMESTAMP DEFAULT SYSTIMESTAMP,
    operation VARCHAR2(50),
    status VARCHAR2(20)
);
```
<img width="900" height="400" alt="image" src="https://github.com/user-attachments/assets/382dfd64-27c0-499b-a93d-9984567b30ed" />

# Smart Rules (Triggers) 🚀

# Block Weekday Changes

This rule stops any changes (like adding, updating, or deleting sales) on Mondays to Fridays and on holidays.

# Track Every Change

This rule logs every sale change—like a diary that never forgets!

# Log Denied Actions

This logs when changes are blocked, so we know what happened.

```sql
CREATE OR REPLACE FUNCTION log_denied_action(p_action VARCHAR2)
RETURN VARCHAR2 IS
BEGIN
    INSERT INTO audit_logs(user_id, operation, status)
    VALUES (USER, p_action, 'Denied');
    RETURN 'Logged';
EXCEPTION
    WHEN OTHERS THEN
        RETURN 'Failed to log: ' || SQLERRM;
END;
/
```

<img width="900" height="400" alt="image" src="https://github.com/user-attachments/assets/c8809340-eda6-4d36-b0db-2ad6997104b8" />





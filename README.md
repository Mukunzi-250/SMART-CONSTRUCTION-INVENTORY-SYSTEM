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

**5.TABLE deliveries**: CREATE TABLE deliveries (delivery_id NUMBER PRIMARY KEY,delivery_date DATE DEFAULT SYSDATE NOT NULL,supplier_id NUMBER REFERENCES suppliers(supplier_id),material_id NUMBER REFERENCES materials(material_id),quantity_delivered NUMBER NOT NULL,received_by VARCHAR2(100),status VARCHAR2(20) DEFAULT 'Received');

**6.TABLE holidays**: CREATE TABLE holidays (holiday_date DATE PRIMARY KEY,description VARCHAR2(100));

**7.TABLE audit_logs**: CREATE TABLE audit_logs (audit_id NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,user_id VARCHAR2(50),action_time TIMESTAMP DEFAULT SYSTIMESTAMP,table_name VARCHAR2(50),operation VARCHAR2(20),old_values CLOB,new_values CLOB);

**8.TABLE stock_alerts**: CREATE TABLE stock_alerts (alert_id NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,material_id NUMBER REFERENCES materials(material_id),alert_type VARCHAR2(50),alert_message VARCHAR2(200),alert_date DATE DEFAULT SYSDATE,resolved CHAR(1) DEFAULT 'N');

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



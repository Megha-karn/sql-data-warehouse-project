# Data Catalog for Gold Layer

## Overview
The **Gold Layer** is the business-level data representation, structured to support analytical and reporting use cases.  
It consists of **dimension tables** and **fact tables** that provide clean, enriched, and business-friendly data models for specific business metrics.

---
1. gold.dim_customers
Purpose: Stores customer details enriched with demographic and geographic data.

Columns:

| Column Name      | Data Type     | Description                                                                 |
|------------------|---------------|-----------------------------------------------------------------------------|
| **customer_key** | `INT` (PK)    | Surrogate key uniquely identifying each customer record in the dimension table (primary key, auto-incremented). |
| **customer_id**  | `INT`         | Unique numerical identifier assigned to each customer (often from source system). |
| **customer_number** | `NVARCHAR(50)` | Alphanumeric identifier representing the customer, used for tracking and referencing. |
| **first_name**   | `NVARCHAR(50)` | The customer’s first name.                                                  |
| **last_name**    | `NVARCHAR(50)` | The customer’s last name or family name.                                    |
| **country**      | `NVARCHAR(50)` | Country of residence (e.g., "Australia").                                   |
| **marital_status** | `NVARCHAR(50)` | Marital status (e.g., "Married", "Single").                                |
| **gender**       | `NVARCHAR(50)` | Gender of the customer (e.g., "Male", "Female", "n/a").                     |
| **birthdate**    | `DATE`         | Date of birth (YYYY-MM-DD).                                                 |
| **create_date**  | `DATETIME`     | Date and time when the customer record was created in the system.           |

2. gold.dim_products
Purpose: Provides information about the products and their attributes.

Columns:

| Column Name          | Data Type      | Description                                                                 |
|----------------------|----------------|-----------------------------------------------------------------------------|
| **product_key**      | `INT` (PK)     | Surrogate key uniquely identifying each product record in the product dimension table. |
| **product_id**       | `INT`          | A unique identifier assigned to the product for internal tracking and referencing. |
| **product_number**   | `NVARCHAR(50)` | Structured alphanumeric code representing the product, often used for categorization or inventory. |
| **product_name**     | `NVARCHAR(50)` | Descriptive name of the product, including details such as type, color, and size. |
| **category_id**      | `NVARCHAR(50)` | Unique identifier for the product’s category, linking to its high-level classification. |
| **category**         | `NVARCHAR(50)` | Broader classification of the product (e.g., *Bikes*, *Components*).        |
| **subcategory**      | `NVARCHAR(50)` | More detailed classification of the product within the category (e.g., *Mountain Bikes*). |
| **maintenance_required** | `NVARCHAR(50)` | Indicates whether the product requires maintenance (e.g., `Yes`, `No`).    |
| **cost**             | `INT`          | Cost or base price of the product, measured in monetary units.              |
| **product_line**     | `NVARCHAR(50)` | The specific product line or series to which the product belongs (e.g., *Road*, *Mountain*). |
| **start_date**       | `DATE`         | The date when the product became available for sale or use.                 |


3. gold.fact_sales
Purpose: Stores transactional sales data for analytical purposes.

Columns:

| Column Name     | Data Type      | Description                                                                 |
|-----------------|----------------|-----------------------------------------------------------------------------|
| **order_number** | `NVARCHAR(50)` | Unique alphanumeric identifier for each sales order (e.g., `SO54496`).      |
| **product_key**  | `INT` (FK)     | Surrogate key linking the order to the **Product Dimension** (`DimProduct`). |
| **customer_key** | `INT` (FK)     | Surrogate key linking the order to the **Customer Dimension** (`DimCustomer`). |
| **order_date**   | `DATE`         | The date when the order was placed.                                         |
| **shipping_date**| `DATE`         | The date when the order was shipped to the customer.                        |
| **due_date**     | `DATE`         | The date when the order payment was due.                                    |
| **sales_amount** | `INT`          | Total monetary value of the sale for the line item, in whole currency units (e.g., 25). |
| **quantity**     | `INT`          | Number of units of the product ordered for the line item (e.g., 1).         |
| **price**        | `INT`          | Price per unit of the product for the line item, in whole currency units (e.g., 25). |

# Marketing Analysis for Motion International Company showcasing product and sales performance.
The company has requested to know their sales performance over the years across various dimensions. This project uses SQL to gather their reporting requirements and provide actionable insights for the data-driven business decisions.

![](SQL_Image.jpeg)

## Introduction:
This project analyses the sales, products, manufacturers, geographical locations, and customers datasets of a supply chain company, Motion International COmpany using SQL. The goal is to replicate a wireframe provided by the Business Analyst in consultation with the Senior Management to provide yearly insights into products, sales, geographical location performances and tailor marketing strategies to meet the business needs.

Disclaimer ⚠️: The dataset used and reports generated do not represent any company, institution, or country. It is a dummy dataset used to showcase proficiency with SQL.

## Problem Statement:
### Question 1. ---  Generate the following measures for the year 2013 and 2014 by month:
a. total sales,
b. rolling total,
c. total sales year to date difference,
d. percentage total sales year to date difference

### Question 2. --- Generate the total sales and percentage of total sales for year 2014 by region and channel. 

### Question 3. --- Generate the total sales, total vanarsdel sales and vanarsdel market share by state.

## Proficient SQL Skills:

CREATE and USE Database
SELECT, SELECT DISTINCT, FROM, WHERE clauses
CASE WHEN
CTE (WITH)
COALESCE, JOIN, ON
DISTINCT COUNT
NULIF, ROUND(AVG()
REPLACE, UPDATE, SET
AND, OR, IS NULL, GREATER/LESS THAN, EQUAL TO
CASE, WHEN, THEN
ALTER TABLE, ADD, VARCHAR

Data Analysis:
1. Creating the database
I created a database and tited it "practice". Then I ensured the database created was selected. The dataset "employee_review" was already saved on my computer. This was imported into the "practice" database. I refreshed the database and ensured the table appeared.





                                        create schema  capstone_project;
                                        use capstone_project;
                                        
                                        -- 1. Ingesting category table 
                                        
                                        CREATE TABLE category (
                                        category text,
                                        channel text,
                                        sort INT
                                        );
                                        LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/capstone_project/Category.csv'
                                        INTO TABLE category
                                        FIELDS TERMINATED BY ','
                                        ENCLOSED BY '"'
                                        LINES TERMINATED BY '\n'
                                        IGNORE 1 ROWS;
                                        -- creating indexes
                                        create index idx_segment
                                        ON category (category(100));
                                        
                                        
                                        -- 2. Ingesting geographical_locations table
                                        
                                        CREATE TABLE geographical_locations (
                                        Zip INT,
                                        City text,
                                        State text,
                                        Region text,
                                        District text
                                        );
                                        -- drop table geographical_locations;
                                        LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/capstone_project/geographical_locations.csv'
                                        INTO TABLE geographical_locations
                                        FIELDS TERMINATED BY ','
                                        ENCLOSED BY '"'
                                        LINES TERMINATED BY '\n'
                                        IGNORE 1 ROWS;
                                        -- creating indexes
                                        create index idx_geo
                                        ON geographical_locations (zip);
                                        
                                        -- 3. Ingesting date table
                                        
                                        CREATE TABLE date (
                                        Date date,
                                        MonthNo INT,
                                        MonthName text,
                                        MonthID INT,
                                        Monthyear text,
                                        Quarter text,
                                        Year INT,
                                        MonthIndex INT,
                                        Months text
                                        );
                                        -- drop table date;
                                        LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/capstone_project/Date.csv'
                                        INTO TABLE date
                                        FIELDS TERMINATED BY ','
                                        ENCLOSED BY '"'
                                        LINES TERMINATED BY '\n'
                                        IGNORE 1 ROWS;
                                        create index idx_date
                                        ON date (date);
                                        create index idx_monthno
                                        ON date (monthno);
                                        
                                        -- 4. Ingesting manufacturer table
                                        
                                        CREATE TABLE manufacturer (
                                        manufacturerid INT,
                                        manufacturer text,
                                        mfgisvanarsdel text
                                        );
                                        -- drop table date;
                                        LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/capstone_project/manufacturer.csv'
                                        INTO TABLE manufacturer
                                        FIELDS TERMINATED BY ','
                                        ENCLOSED BY '"'
                                        LINES TERMINATED BY '\n'
                                        IGNORE 1 ROWS;
                                        
                                        -- 5. Ingesting motion sales table
                                        
                                        CREATE TABLE motion_sales (
                                        productid INT,
                                        date date,
                                        Zip INT,
                                        Units INT,
                                        Revenue decimal(22,7)
                                        );
                                        LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/capstone_project/motion_sales.csv'
                                        INTO TABLE motion_sales
                                        FIELDS TERMINATED BY '\t'
                                        ENCLOSED BY '"'
                                        LINES TERMINATED BY '\n'
                                        IGNORE 1 ROWS;
                                        -- Creating indexes
                                        create index idx_geo
                                        ON motion_sales (zip);
                                        create index idx_productid
                                        ON motion_sales (productid);
                                        create index idx_date
                                        ON motion_sales (date);
                                        
                                        -- 6. Ingesting products table
                                        
                                        CREATE TABLE products (
                                        manufacturer text,
                                        category text,
                                        segment text,
                                        product text,
                                        productid INT,
                                        isvanrrsdel text,
                                        iscompetehide text,
                                        manufacturerid INT,
                                        iscompete text
                                        );
                                        -- drop table motion_sales;
                                        LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/capstone_project/products.csv'
                                        INTO TABLE products
                                        FIELDS TERMINATED BY ','
                                        ENCLOSED BY '"'
                                        LINES TERMINATED BY '\n'
                                        IGNORE 1 ROWS;
                                        -- creating indexes
                                        create index idx_productid
                                        ON products (productid);
                                        create index idx_segment
                                        ON products (segment(100));

# Library-Operations-Performance-Analytics-SQL-Project-

## Project Overview

This project focuses on building a relational library database using SQL. It involves designing and managing multiple related tables, performing CRUD operations, and writing analytical queries to generate insights from the data. The purpose of this project is to demonstrate practical skills in database design, data manipulation, and advanced SQL querying within a real-world scenario.


## Objectives

- Design and implement a relational database to simulate a multi-branch library system
- Perform CRUD operations: Creat, Read, Update, Delete to efficiently manage and manipulate data
- Utilize CTAS (Create Table As Select) to create summary and reporting tables

## Project Structure
### 1. Database Design
![Library ERD](https://github.com/merveillemoke/Library-Operations-Performance-Analytics-SQL-Project-/blob/main/Library%20ERD.png)

- Database Creation
- Table Creation: I Created tables for branches, employees, members, books, issued status, and return status
```sql
  -- Library Operations Performance Analytics Tables Creation

-- Creating Branch Table
DROP TABLE IF EXISTS branch;
CREATE TABLE branch(
	branch_id VARCHAR(10) PRIMARY KEY,
	manager_id VARCHAR(10),
	branch_address VARCHAR(55),
	contact_no VARCHAR(20)
);

-- Creating Employees Table
DROP TABLE IF EXISTS employees;
CREATE TABLE employees(
	emp_id VARCHAR(10) PRIMARY KEY,
	emp_name VARCHAR(25),
	position VARCHAR(25),
	salary INT,
	branch_id VARCHAR(25), -- FK
	FOREIGN KEY (branch_id) REFERENCES branch(branch_id)
);

-- Creating Books table
DROP TABLE IF EXISTS books;
CREATE TABLE books(
	isbn VARCHAR(20) PRIMARY KEY, 
	book_title VARCHAR(75), 
	category VARCHAR(20), 
	rental_price FLOAT, 
	status VARCHAR(15), 
	author VARCHAR(35), 
	publisher VARCHAR(55)
);

-- Creating Members table
DROP TABLE IF EXISTS members;
CREATE TABLE members(
	member_id VARCHAR(20) PRIMARY KEY,
	member_name VARCHAR(25),
	member_address VARCHAR(75),
	reg_date DATE
);

--Creating issued_status table
DROP TABLE IF EXISTS issued_status;
CREATE TABLE issued_status(
	issued_id VARCHAR(10) PRIMARY KEY,
	issued_member_id VARCHAR(10), -- FK
	issued_book_name VARCHAR(75),
	issued_date DATE,
	issued_book_isbn VARCHAR(25), -- FK
	issued_emp_id VARCHAR(10), -- FK
	FOREIGN KEY (issued_member_id) REFERENCES members(member_id),
	FOREIGN KEY (issued_book_isbn) REFERENCES books(isbn),
	FOREIGN KEY (issued_emp_id) REFERENCES employees(emp_id)
);

-- Creating return_status table
DROP TABLE IF EXISTS return_status;
CREATE TABLE return_status(
	return_id VARCHAR(10) PRIMARY KEY,
	issued_id VARCHAR(10), -- FK
	return_book_name VARCHAR(75),
	return_date DATE,
	return_book_isbn VARCHAR(20),
	FOREIGN KEY (issued_id) REFERENCES issued_status(issued_id)
);
```

## 2. CRUD Operations
- Create
- Read
- Update
- Delete

#### Task 1: Create a new book record
```sql
Insert INTO books(isbn, book_title, category, rental_price, status, author, publisher)
VALUES 
	('978-0-7432-7356-5','The Alchemist','Fiction', 5.50, 'yes','Paulo Coelho','HarperOne');
```

#### Task 2: Retrieve all available books - Select books where status = 'yes'
```sql
SELECT *
FROM books
WHERE status = 'yes';
```

#### Task 3: Update Member Address - Modify the address of an existing member
```sql
UPDATE members
SET member_address = '125 Main St'
WHERE Member_id = 'C101';
```

#### Task 4: Delete a record from the issue status table
Delete the record with issued_id = 'IS121' from the issued_status table
```sql
DELETE FROM issued_status
WHERE issued_id = 'IS121';
```
## 3. CTAS(Create Table As Select)
### Task 5: Create Summary Tables: Use CTAS to create a new table based on the query results - each book and total book_issued_cnt
```sql
CREATE TABLE book_cnts AS
SELECT
	b.isbn,
	b.book_title,
	COUNT(ist.issued_id) as no_issued
FROM books as b
JOIN
issued_status as ist
ON ist.issued_book_isbn = b.isbn
GROUP BY 1, 2
```

## Project Summary
This project demonstrates the practical application of SQL in designing tand managing a relational database system. It combines database design, data manipulation, and analytical querying. 



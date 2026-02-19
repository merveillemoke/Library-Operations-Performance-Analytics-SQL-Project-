# Library-Operations-Performance-Analytics-SQL-Project-

## Project Overview

This project focuses on building a relational library database using SQL. It involves designing and managing multiple related tables, performing CRUD operations, and writing analytical queries to generate insights from the data. The purpose of this project is to demonstrate practical skills in database design, data manipulation, and advanced SQL querying within a real-world scenario.


## Objectives

- Design and implement a relational database to simulate a multi-branch library system
- Perform CRUD operations: Creat, Read, Update, Delete to efficiently manage and manipulate data
- Utilize CTAS (Create Table As Select) to create summary and reporting tables
- Develop advanced SQL queries to analyze data and extract meaningful insights

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
	issued_id VARCHAR(10),
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
```

#### Task 2: Retrieve all available books - Select books where status = 'yes'
```sql
```

#### Task 3: Update Member Address - Modify the address of an existing member
```sql
```

```sql
```

#### Task 4: Delete a record from the issue status table
```sql
```



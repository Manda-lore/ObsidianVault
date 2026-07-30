- # Introduction to SQL
	- SQL - Structured Query Language
	- SQL has two types of databases
		- Relational Databases
		- Non Relational Databases
	- We need DBMS to use write and manage databases
- # Database Operations - Basic
	- creating database with name mydb
		- ```mysql
		  create database mydb;
		  ```
	- use <mydb>;
		- ```mysql
		  use mydb;
		  ```
	- drop database <mydb>;
		- ```mysql
		  drop database mydb;
		  ```
	- alter database <mydb> read only = 1; (makes the database read only)
		- ```mysql
		  alter database mydb read only = 1;
		  ```
- # Table Operations - Basic
	- Table Creation
		- ```mysql
		  create table employee (
		    employee_id int,
		    first_name varchar(50),
		    last_name varchar(50),
		    hourly_pay decimal(5,2),
		    hire_date date
		  );
		  ```
	- Select Table
		- ```mysql
		  select * from employees;
		  ```
	- Rename table
		- ```mysql
		  rename table employees to Employees;
		  ```
	- Drop table
		- ```mysql
		  drop table Employees;
		  ```
	- Alter table
		- ```mysql
		  alter table employees
		  add phone_number varchar(15);
		  
		  alter table employees
		  rename column phone_number to email;
		  
		  alter table employees
		  modify column email varchar(100);
		  
		  alter table employees
		  modify email varchar(100)
		  after last_name
		  
		  alter table employees
		  drop column email;
		  ```
	- Insert Rows
		- ```mysql
		  insert into employees
		  values
		    (1, "Eugene", "Krabs", 25.50, "2023-01-02"),
		    (2, "Spongebob", "Squarepants", 12.50, "2023-01-05");
		    
		   insert into employees (employee_id, first_name, last_name)
		   values (6, "Sheldon", "Plankton");
		  ```
	- Select Operations - Basic
		- ```mysql
		  select first_name, last_name
		  from employees
		  where employee_id = 1;
		  
		  select *
		  from employees
		  where hire_date is null;
		  ```
	- Update Rows
		- ```mysql
		  update employees;
		  set hourly_pay = 10.25,
		  	hire_date = "2023-01-7",
		      last_name = null
		  where employee_id = 6;
		  ```
	- Delete Rows
		- ```mysql
		  delete from employees
		  where employee_id = 4;
		  ```
- # Autocommit and Manual Commit
	- ```mysql
	  set autocommit = off
	  commit
	  rollback
	  ```
- # Current Date and Time
	- ```mysql
	  insert into test
	  values (current_date(), current_time(), now());
	  ```
- # Constraints in DBMS
	- Unique
		- ```mysql
		  create table products (
		    product_id int,
		    product_name varchar(25) unique,
		    price decimal(4, 2)
		  );
		  
		  alter table products
		  add constraint
		  unique (product_name);
		  ```
	- Not Null
		- ```mysql
		  create table products (
		    product_id int,
		    product_name varchar(25),
		    price decimal(4,2) not null
		  );
		  
		  alter table products
		  modify price decimal (4,2) not null;
		  ```
	- Check
		- ```mysql
		  create table employee (
		    employee_id int,
		    first_name varchar(50),
		    last_name varchar(50),
		    hourly_pay decimal(5,2),
		    hire_date date,
		    constraint chk_hourly_pay check (hourly_pay >= 10.00)
		  );
		  
		  alter table employee
		  add constraint chk_hourly_pay check (hourly_pay >=  10.00)
		  
		  alter table employee
		  drop check chk_hourly_pay
		  ```
	- Default
		- ```mysql
		  create table products (
		    product_id int,
		    product_name varchar(25),
		    price decimal(4,2) default 1.00
		  );
		  
		  alter table products
		  alter price set default 1.00
		  
		  create table transactions (
		    transaction_id int,
		    amount decimal(5, 2),
		    transaction_date datetime default now()
		  );
		  ```
	- Primary Key
		- id:: 6a673395-1bc7-4aea-8114-7ece4c04d69a
		  ```mysql
		  create table transactions (
		    transaction_id int primary key,
		    amount decimal (5, 2)
		  );
		  
		  alter table transactions
		  add constraint
		  primay key (transaction_id);
		  ```
	- Auto Increment
		- ```mysql
		  create table transactions (
		    transaction_id int primary key auto_increment,
		    amount decimal (5, 2)
		  );
		  
		  alter table transactions
		  auto_increment = 1000
		  ```
	- Foreign Key
		- ```mysql
		  create table customers (
		    customer_id int primary key auto_increment,
		    first_name varchar(50),
		    last_name varchar(50)
		  );
		  
		  create table transactions (
		    transaction_id int primary key,
		    amount decimal (5, 2),
		    customer_id int,
		    constraint customer_fk foreign key (customer_id) references customers(customer_id)
		  );
		  
		  alter table transactions
		  drop foreign key customer_fk;
		  
		  alter table transactions
		  add constraint fk_customer_id
		  foreign key (customer_id) references customers(customer_id)
		  ```
- # Joins in DBMS
	- Inner Join
		- ```MySQL
		  select transaction_id, amount, first_name, last_name
		  from transactions inner join customers
		  on transactions.customer_id = customers.customer_id;
		  ```
	- Left Join
		- ```MySQL
		  select transaction_id, amount, first_name, last_name
		  from transactions left join customers
		  on transactions.customer_id = customers.customer_id;
		  ```
	- Right Join
		- ```MySQL
		  select transaction_id, amount, first_name, last_name
		  from transactions right join customers
		  on transactions.customer_id = customers.customer_id;
		  ```
- # Function in MySQL - Basic
	- Count
		- ```MySQL
		  select count(amount) as "total transactions"
		  from transactions;
		  ```
	- Max
		- ```MySQL
		  select max(amount) as "max amount"
		  from transactions;
		  ```
	- Min
		- ```MySQL
		  select min(amount) as "min amount"
		  from transactions;
		  ```
	- Avg
		- ```MySQL
		  select avg(amount) as "avg amount"
		  from transactions;
		  ```
	- Sum
		- ```MySQL
		  select sum(amount) as "total amount"
		  from transactions;
		  ```
	- Concat
		- ```MySQL
		  select concat(first_name," ", last_name) as full_name
		  from employees;
		  ```
- # Logical Operators in MySQL
	- ```MySQL
	  select *
	  from employees
	  where hire_date < "2023-01-5" and job = "cook";
	  
	  select *
	  from employees
	  where job = "cook" or job = "cashier";
	  
	  select *
	  from employees
	  where not job = "manager" and not job = "asst. manager";
	  
	  select *
	  from employees
	  where hire_date between "2023-01-04" and "2023-01-07";
	  
	  select *
	  from employees
	  where job in ("cook", "cashier", "janitor");
	  ```
- # Wild Card Characters (% _)
	- Used to substitute one or more characters in a string
	- ```MySQL
	  select * from employees
	  where first_name like "s%";
	  
	  select * from employees
	  where hire_date like "____-01-__";
	  
	  select * from employees
	  where job like "_a%";
	  ```
- # Order By Clause in MySQL
	- ```MySQL
	  select * from employees
	  order by last_name;
	  
	  select * from employees
	  order by last_name desc;
	  ```
- # Limit Clause in MySQL
	- ```MySQL
	  select * from customers
	  limit 5;
	  
	  select * from customers
	  order by last_name desc
	  limit 5;
	  
	  select * from customers
	  limit 3, 1; #offsets by 3 records and limits the output to 1
	  ```
- # Union Operator in MySQL
	- ```MySQL
	  select first_name, last_name from employees
	  union
	  select first_name, last_name from customers;
	  ```
	- <union> doesnot allow duplicates but you can use <union all> to allow duplicates
- # Self Join in MySQL
	- ```MySQL
	  select *
	  from customers as a
	  inner join customers as b
	  on a.referral_id = b.customer_id;
	  ```
	- is created with inner join, left join, right join as per requirement
- # Views in MySQL
	- views are virtual tables based on the result set of sql statement
	- view tables are not real tables but they can be interacted or used as if they are real tables
	- ```MySQL
	  create view employee_attendance as
	  select first_name, last_name
	  from employees;
	  
	  select * from employee_attendance;
	  drop view employee_attendance;
	  ```
	- views are updated when a real table is updated
- # Index in MySQL
	- Indexes are used to find values within specific columns more quickly
	- MySQL normally searches sequentially through a column, the longer the column the more expensive the operation
	- update takes more time, select takes less time with index
	- ```MySQL
	  show indexes from customers;
	  
	  create index last_name_idx
	  on customers(last_name);
	  
	  create index last_name_first_name_idx
	  on customers(last_name, first_name);
	  
	  alter table customers
	  drop index last_name_idx;
	  ```
- # Sub Queries in MySQL
	- A query within a query is sub query
	- ```MySQL
	  select first_name, last_name, hourly_pay,
	  	(select avg(hourly_pay) from employees as avg_pay)
	  from employees;
	  
	  select first_name, last_name< hourly_pay
	  from employees
	  where hourly_pay >	(select avg(hourly_pay) from employees);
	  
	  select first_name, last_name
	  from customers
	  where customer_id in
	  (select distinct customer_id
	  from transactions
	  where customer_id is not null);
	  ```
- # Group By Clause in MySQL
	- group rows based on specific column, often used with `sum()`, `max()`, `min()`, `avg()`, `count()`
	- ```MySQL
	  select sum(amount), order_date
	  from transactions
	  group by order_date;
	  ```
	- you cannot use `where` clause with `group by` clause instead use `having` clause
		- ```MySQL
		  select count(amount), customer_id
		  from transactions
		  group by customer_id
		  having count(amount > 1) and customer_id is not null;
		  ```
- # Rollup clause in MySQL
	- extension of group by clause, produces another row and shows the grand total (super aggregate value) of columns
	- ```MySQL
	  select count(transaction_id) as "no of orders", customer_id
	  from transactions
	  group by customer_id with rollup;
	  
	  select employee_id, sum(hourly_pay)
	  from employees
	  group by employee_id with rollup;
	  ```
- # On Delete clause in MySQL
	- 2 types
		- on delete set null = when fk is deleted, replace fk with null
		- on delete cascade = when fk is deleted, delete row
	- ```MySQL
	  # when creating a table
	  create table transactions (
	    tranaction_id int primary key,
	    amount decimal (5,2),
	    customer_id int,
	    order_date date,
	    foreign key (customer_id) references customers(customer_id)
	    on delete set null #or on delete cascade
	  );
	  
	  # adding on delete clause to existing table
	  alter table transactions drop foreign key fk_customer_id
	  alter table transactions
	  add constraint fk_customer_id
	  foreign key(customer_id) references customers(customer_id)
	  on delete set null; #or on delete cascade
	  ```
- # Stored Procedures
	- we can save an often used sql query as stored procedure
	- ```MySQL
	  delimiter $$
	  create procedure get_customers()
	  begin
	  	select * from customers;
	  end $$
	  delimiter ;
	  
	  call getcustomers();
	  
	  drop procedure get_customers;
	  
	  delimiter $$
	  create procedure find_customer(in id int)
	  begin
	  	select * from customers
	      where customer_id = id;
	  end $$
	  delimiter ;
	  
	  call find_customer(1);
	  drop procedure find_customer;
	  
	  delimiter $$
	  create procedure find_customer(in f_name varchar(50), in l_name varchar(50))
	  begin
	  	select * from customers
	  	where first_name = f_name and last_name = l_name;
	  end $$
	  delimiter ;
	  
	  call find_customer("Nissi", "G");
	  ```
	- secure, but increases memory usage per connection
- # Triggers in MySQL
	- triggers automatically execute a query when something user defined happens
	- like updating hourly_pay automatically updates the salary
	- ```MySQL
	  # before trigger
	  create trigger before_hourly_pay_update
	  before update on employees
	  for each row
	  set new.salary = (new.hourly_pay * 2080)
	  
	  # after trigger
	  create trigger after_salary_delete
	  after delete on employees
	  for each row
	  update expenses
	  set expense_total = expense_total - old.salary
	  where expense_name = "salaries";
	  ```

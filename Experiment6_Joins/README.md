# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**

From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission.

Sample table: orders

![image](https://github.com/user-attachments/assets/81dc001a-6cad-4fe9-b1c0-1762b487e660)

```
select o.ord_no,

o.ord_date,

o.purch_amt,

c.cust_name as 'Customer Name',

c.grade,

s.name as Salesman,

s.commission

from orders as o

join customer c on o.customer_id=c.customer_id

join salesman s on o.salesman_id=s.salesman_id;

```

**Output:**

![image](https://github.com/user-attachments/assets/9db90081-3889-481b-8a63-063f1911b36a)

**Question 2**

write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

![image](https://github.com/user-attachments/assets/9a97cee8-1214-415f-9b2f-0d832ef71ae1)

```
select s.name as Salesman,c.cust_name,c.city

from salesman s

join customer c on s.city=c.city;

```

**Output:**

![image](https://github.com/user-attachments/assets/bd97e929-e890-4ae9-8f1a-9b7c09f45094)

**Question 3**

Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a null discharge date.

![image](https://github.com/user-attachments/assets/7fa5c1fd-9807-4bb3-bc0e-9fc970ea14de)

```
select p.first_name as "patient_name",d.first_name as doctor_name

from patients p

inner join doctors d on p.doctor_id=d.doctor_id

where p.discharge_date is null;

```

**Output:**

![image](https://github.com/user-attachments/assets/0e95bf20-f118-4b91-8f41-a5a24e272949)

**Question 4**

Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the city 'New York'.

![image](https://github.com/user-attachments/assets/400ff890-74f6-4fbd-bfe1-3259fab4138a)

```
select s.name

from salesman s

left join customer c on s.salesman_id=c.salesman_id

where c.city='New York';

```

**Output:**

![image](https://github.com/user-attachments/assets/63af043c-8ef6-445a-831a-526fda71f7cc)

**Question 5**

From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.

Sample table: customer

![image](https://github.com/user-attachments/assets/b40fe0c7-d4d0-485d-85c5-fe3aa77c1718)

```
select c.cust_name,

c.city,

c.grade,

s.name AS Salesman,

s.city

from customer c

join salesman as s ON s.salesman_id=c.salesman_id

order by customer_id ASC;

```

**Output:**

![image](https://github.com/user-attachments/assets/0f37f3df-1e35-48b0-b6ac-39cd1c55dcda)

**Question 6**

Write the SQL query that achieves the selection of the "cust_name" and "city" columns from the "customer" table (aliased as "c"), and the "ord_no," "ord_date," and "purch_amt" columns from the "orders" table (aliased as "o"), with a left join on the "customer_id" column and a condition filtering for customers in the city 'London'.

![image](https://github.com/user-attachments/assets/3b05597e-6002-4757-b10b-37f19bbbd3fb)

```
select c.cust_name,

c.city,

o.ord_no,

o.ord_date,

o.purch_amt

from customer c

left join orders o ON c.customer_id=o.customer_id

where c.city = 'London';

```

**Output:**

![image](https://github.com/user-attachments/assets/b19f9a36-ad8f-49bd-81dd-980c6451e01f)

**Question 7**

Write the SQL query that achieves the selection of all columns from the "nurses" table (aliased as "n") and the "department_name" column from the "departments" table, with an inner join on the "department_id" column.

NURSES TABLE:

![image](https://github.com/user-attachments/assets/4aa540ef-ed17-461b-ae62-0474de8f37f1)

```
d.department_name

from nurses n

inner join departments d ON n.department_id=d.department_id;

```

**Output:**

![image](https://github.com/user-attachments/assets/0d591d57-d5df-4825-a2a8-13bf8bab8371)

**Question 8**

From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission

![image](https://github.com/user-attachments/assets/b0d391b8-679e-4b14-b010-3d6596aaf11d)

```
select c.cust_name AS "Customer Name",

c.city,

s.name as "Salesman",

s.commission

from customer c

inner join salesman s ON c.salesman_id=s.salesman_id;

```

**Output:**

![image](https://github.com/user-attachments/assets/fdf2f86c-5390-45b5-9ca7-2b0f3d4604a9)

**Question 9**

Write a SQL statement to make a report with customer name, city, order number, order date, and order amount in ascending order according to the order date to determine whether any of the existing customers have placed an order or not.

![image](https://github.com/user-attachments/assets/a30c191e-d742-4f5f-90be-6cac65acd6cd)

```
select a.cust_name,a.city,b.ord_no,

b.ord_date,b.purch_amt as "Order Amount"

from customer a

left outer join orders b ON a.customer_id=b.customer_id

order by b.ord_date ;

```

**Output:**

![image](https://github.com/user-attachments/assets/20e43983-534e-443b-a9fe-725ffecbcb4b)

**Question 10**

Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for appointments with an appointment date between '2024-02-01' and '2024-02-28'.

![image](https://github.com/user-attachments/assets/423a422a-c1ae-42e3-8f54-71edd3f1cbe4)

```
select p.*

from patients p

inner join appointments a ON p.patient_id =a.patient_id

where a.appointment_date BETWEEN

'2024-02-01'AND '2024-02-28';

```

**Output:**

![image](https://github.com/user-attachments/assets/3706674a-4ed1-4b47-acaf-816e83a6913c)

## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.

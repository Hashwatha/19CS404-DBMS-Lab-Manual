# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**

Write a SQL query to Retrieve the medications with dosages equal to the highest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)

![image](https://github.com/user-attachments/assets/b50adfac-9051-4514-9340-91fee9632976)

```
select medication_id as medic,medication_name,dosage

from Medications

where dosage=(select max(dosage)

from Medications );
```

**Output:**

![image](https://github.com/user-attachments/assets/05d1de98-ea29-4492-856d-67873df8daa5)

**Question 2**

Write a SQL query to List departments with names longer than the average length

Departments Table (attributes: department_id, department_name)

![image](https://github.com/user-attachments/assets/8f9511a7-f3a2-4d83-9e1e-b31dc7880d68)

```
select department_id, department_name

from Departments

where length(department_name)>(select avg(length(department_name))

from Departments );
```

**Output:**

![image](https://github.com/user-attachments/assets/09bcf6a4-20f4-4d3b-8d56-f6c01fe72441)

**Question 3**

Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table

![image](https://github.com/user-attachments/assets/5d20719c-4002-46fb-a95e-98ff24ca6510)

```
select * from Employee

where age<(select avg(age)

from Employee

where income > 250000);
```

**Output:**

![image](https://github.com/user-attachments/assets/77a429a3-5818-424b-9f84-cc50238833e1)

**Question 4**

From the following tables, write a SQL query to find all the orders issued by the salesman 'Paul Adam'. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

salesman table

![image](https://github.com/user-attachments/assets/9e6e267a-7ca0-40b7-929b-180e24be6a8f)

```
select o.ord_no,o.purch_amt,o.ord_date,o.customer_id,o.salesman_id

from Orders as o

join Salesman as s on o.salesman_id=s.salesman_id

where s.name='Paul Adam';

```

**Output:**

![image](https://github.com/user-attachments/assets/5d4ff2a9-3849-4762-9888-baab0ce97f98)

**Question 5**

Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

![image](https://github.com/user-attachments/assets/14d01902-125a-4885-a688-5db4d03eb4d8)

```
select * from CUSTOMERS

where salary in(select SALARY

from CUSTOMERS

where SALARY<2500 );

```

**Output:**

![image](https://github.com/user-attachments/assets/8629049a-bd5e-4f54-a12a-50e2ba7f4ba9)

**Question 6**

From the following tables write a SQL query to count the number of customers with grades above the average in New York City. Return grade and count.

![image](https://github.com/user-attachments/assets/c6dc7af0-3124-40b2-a5e2-8164eae2db09)

```
select grade,COUNT(*)

from customer

where grade>(select avg(grade)

from customer

where city='New York'

)group by grade;

```

**Output:**

![image](https://github.com/user-attachments/assets/9e13de1b-fde2-4b1b-b9d9-ef346b30e63d)

**Question 7**

Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

![image](https://github.com/user-attachments/assets/93930713-23b7-4453-83a8-5bf9aee99635)

```
select g.student_id,g.student_name,g.subject,g.grade

from GRADES as g

where g.grade=(select max(grade)

from GRADES

where subject=g.subject)

order by g.student_name,g.grade;

```

**Output:**

![image](https://github.com/user-attachments/assets/a79a412e-cea2-4106-bcd6-505dfa7b1f07)

**Question 8**

Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

![image](https://github.com/user-attachments/assets/22a20e82-41df-4e52-a73f-e6d02c84f241)

```
select g.student_name,g.grade

from GRADES as g

where g.grade=(select min(grade)

from GRADES

where subject=g.subject)

order by g.student_name,g.grade;
```

**Output:**

![image](https://github.com/user-attachments/assets/0f5fdce7-aac0-401d-bbac-3a864a02c83a)

**Question 9**

Write a query to display all the customers whose ID is the difference between the salesperson ID of Mc Lyon and 2001.

![image](https://github.com/user-attachments/assets/4b47f2d4-9ad0-4bf8-b1b3-97f9f207ec17)

```
select *from customer where customer_id=(select(salesman_id-2001)

from salesman

where name='Mc Lyon' );

```

**Output:**

![image](https://github.com/user-attachments/assets/a737fb90-676d-42ba-8971-09a04957262e)

**Question 10**

From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

![image](https://github.com/user-attachments/assets/0cdfebd6-a8d6-4b23-9f4d-8c3ac737d625)

```
select ord_no,purch_amt,ord_date,customer_id,salesman_id

from ORDERS

where purch_amt>(select avg(purch_amt)

from ORDERS

where ord_date='2012-10-10' );
```

**Output:**

![image](https://github.com/user-attachments/assets/107a3bd3-4cf1-4235-95cc-568e86b8ab98)

## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.

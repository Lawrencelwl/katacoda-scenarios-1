We are going to create a new database employee and user bob. And bob is a staff. Therefore, we need to grant privilege to bob in the employees databases. If Bob is an ordinary employee, he will only have basic permissions. If Bob's position is higher, he will have higher authority

Create a new database (name: employees): 
`create database employees;`{{execute}}

Create a new table staff: 
`CREATE TABLE staff ( staff_id int, last_name varchar(255), first_name varchar(255), email varchar(255), password varchar(255) ) engine = innodb default charset = latin1;`{{execute}}

Create user bob: 
`create user 'bob'@'%' identified by 'bob';`{{execute}}


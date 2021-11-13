Grant privilege (normal staff): 
`GRANT SELECT ON employees.* TO 'bob'@'%';`{{execute}}

Before granting privilege, bob cannot select or connect to the employees databases. 

To show grants for bob after grant privilege:
`show grants for 'bob'@'%';`{{execute}}

And bob can use and select on the employees databases after granting privileged. 
`show databases;`{{execute}}

If Bob's position is very high, you can consider giving him full access to employees databases. 
Grant privilege (director): 
`GRANT ALL PRIVILEGES ON employees.* TO 'bob'@'%';`{{execute}}

To show grants for bob after grant privilege: 
`show grants for 'bob'@'%';`{{execute}}

Login mysql as root user: 

`docker exec –it mysql bash` {{execute}}

`Mysql –u root -p` {{execute}}

The general log is used to improve the performance and security of the MySQL Database Server. 

General log is a log that collects all events in the databases. Because the general log records all actions. So, when there is a problem with the database. We can find the problem through the general log.

First, using database ‘mysql’:
`use mysql;`{{execute}}

Second, show the table schema of the general_log table:

`describe general_log;`{{execute}}

For database security. Data backup is a must. And the data is not recommended to be stored locally. This is because when there is a problem with local resources, data will be lost. Therefore, it is generally recommended to store the data on an external hard drive or in the cloud. And you need 2 backups. In order to avoid one of the hard drives has been damaged. 

Full back up:
`docker exec mysql //usr/bin/mysqldump -u root --password=12345 --routines --triggers mysql > test_db_backup.sql`{{execute}}

Recovery:
`cat test_db_backup.sql | docker exec -i mysql //usr/bin/mysql -u root --password=12345 mysql`{{execute}}

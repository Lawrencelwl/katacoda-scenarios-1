In this user manual, user will know how to set up MYSQL, WordPress by docker. After that, user can use the WooCommerce plugin. 

## Task

First, it requests a connection to the wordpress-network. When the network created, it can have a communication between WordPress container and MYSQL container. 

Please input below command in the katacoda:
`docker network create wordpress-network`{{execute}}

Second, it requests to set up a MYSQL container:
`docker run --name mysql -e MYSQL_ROOT_PASSWORD=12345 -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wordpress -e MYSQL_PASSWORD=12345 --network=wordpress-network -v db_data:/var/lib/mysql  -d mysql --general-log=1 --log-output=TABLE`{{execute}}

Third, it requests to download wordpress image:
`docker pull wordpress`{{execute}}

Final, it requests to set up a wordpress container
`docker run -e WORDPRESS_DB_USER=wordpress -e WORDPRESS_DB_PASSWORD=12345 -e WORDPRESS_DB_HOST=mysql:3306 --name wordpress --network=wordpress-network -p 10080:80 -v /tmp/html/:/var/www/html -d wordpress`{{execute}}

You can input the following command to check container of wordpress and MYSQL running or not:
`docker ps `{{execute}}

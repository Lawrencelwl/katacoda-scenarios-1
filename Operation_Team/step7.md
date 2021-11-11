In this task, we will use polyscripting to defend the code injection attacks

Polyscripting is a tool for the wordpress security. When installing Polyscripting in wordpress, it can defend the code injection attacks. It is because Polyscripting is using a zero-trust approach which is a method that does not allow new plugins or new code to be adapted. 
First, it requests to set up wordpress-network:
`docker network create wordpress-network`{{execute}}

Second, it requests to download polyverse/polyscripted-wordpress image:
`docker pull polyverse/polyscripted-wordpress`{{execute}}

Third, it requests to download wordpress image:
`docker pull wordpress`{{execute}}

Four, it requests to set up a MYSQL container:
`docker run --name mysql -e MYSQL_ROOT_PASSWORD=12345 -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wordpress -e MYSQL_PASSWORD=12345 --network=wordpress-network -v db_data:/var/lib/mysql  -d mysql`{{execute}}

Final, it requests to set up a polyverse/polyscripted-wordpress container 
`docker run -d -e WORDPRESS_DB_USER=wordpress -e WORDPRESS_DB_PASSWORD=12345 -e WORDPRESS_DB_HOST=mysql:3306 --name wordpress --network=wordpress-network -p 10080:80  -v $PWD/wordpress:/wordpress polyverse/polyscripted-wordpress`{{execute}}

You can input the following command to check container of polyverse/polyscripted-wordpress and MYSQL running or not.
`docker ps`{{execute}}

When the set up is finished, it can go to host port 10080 to use wordpress. But Polyscripted version request longer time to start it. It is because it will be generating a new PHP language. Therefore, wordpress needs to transfer it.

It will request to have a basic set up when in the wordpress website. If your set up is already, please skip it.

After the set up, it can enter wordpress website. 

Now move to katacoda, you need to start a simulate attack to wordpress. This attack is using a vulnerability from OWASP (Open Web Application Security Project) which is about code injection.

`<?php $myvar = "varname"; $x = $_GET['arg']; eval("\$myvar = \$x;"); ?>`
This is the information about the vulnerable file. 

Now, you need to create a vulnerable file is the katacoda, it is because we are simulate the wordpress has been code injection
`echo "<?php \$myvar = \"varname\"; \$x = \$_GET['arg']; eval(\"\\\$myvar = \$x;\"); ?>" >hack.php`

After, injecting the file to wordpress. When the file is injected into the wordpress, it will be shown like a bug.
`docker cp hack.php wordpress:/var/www/html/`{{execute}}

Check the results in: `/hack.php?arg=1; %echo phpinfo()`
If you see the results in the below, it means attacker extract the information of the private server.

Hackers know how to read this PHP information, and it will be dangerous for the wordpress server. 

Now move to katacoda again and stop the wordpress. It is because we will active polyscripting service. 
`docker stop wordpress`{{execute}}

After stopping the wordpress, you need to remove it and act it again. 
`docker rm wordpress`{{execute}}

When the remove finished, check container of polyverse/polyscripted-wordpress remove or not. 
`docker ps`{{execute}}

After that, you need to set up a polyverse/polyscripted-wordpress container and activation the service of Polyscripting
`docker run -d -e "MODE=polyscripted"  -e WORDPRESS_DB_USER=wordpress -e WORDPRESS_DB_PASSWORD=12345 -e WORDPRESS_DB_HOST=mysql:3306 --name wordpress --network=wordpress-network -p 10080:80  -v $PWD/wordpress:/wordpress polyverse/polyscripted-wordpress`{{execute}}

Now, you can inject the file to wordpress. It will be like attacker attack wordpress again. 
`docker cp hack.php wordpress:/var/www/html/`{{execute}}

Check the results in: `/hack.php?arg=1; %echo phpinfo()`
If you see the results in the below, it means attacker cannot extract the information of the private server. It is because polyscripting blocks new plugins or new code to be adapted. It can let your wordpress to be security!

## Conclusion of polyscripting

Polyscripting is a good tool to defend code injection. But the disadvantage is it will block all new plugins or new code to be adapted. Therefore, if you need to add new plugins or new code. 

Please use Plain wordpress mode in the below command. 
`docker stop wordpress`{{execute}}
`docker rm wordpress`{{execute}}

`docker run -d -e WORDPRESS_DB_USER=wordpress -e WORDPRESS_DB_PASSWORD=12345 -e WORDPRESS_DB_HOST=mysql:3306 --name wordpress --network=wordpress-network -p 10080:80  -v $PWD/wordpress:/wordpress polyverse/polyscripted-wordpress`{{execute}}

You can use Polyscripting wordpress mode after adding new plugins or new code by the follow command.
`docker stop wordpress`{{execute}}
`docker rm wordpress`{{execute}}

`docker run -d -e "MODE=polyscripted"  -e WORDPRESS_DB_USER=wordpress -e WORDPRESS_DB_PASSWORD=12345 -e WORDPRESS_DB_HOST=mysql:3306 --name wordpress --network=wordpress-network -p 10080:80  -v $PWD/wordpress:/wordpress polyverse/polyscripted-wordpress`{{execute}}
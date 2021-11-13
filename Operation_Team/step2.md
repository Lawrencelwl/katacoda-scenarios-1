Now we will setup WordPress for the operation team to use.

When the set up finished, it can go to host port 10080 to use WordPress:
[WordPress on Port 10080](https://[[HOST_SUBDOMAIN]]-10080-[[KATACODA_HOST]].environments.katacoda.com/)

![Step1](./assets/1.png)
When user login to wordpress, it requests to input personal information.

![Step2](./assets/2.png)
After the set up, it can enter wordpress website. The first step is set up the Woocommerce. Woocommerce can help to do online e-commerce store.

First, it needs to add appearance when using Woocommerce. Follow:
Appearance -> Themes -> kick “Add New”
In the Search themes, search storefront and install it to be our e-commerce website.
![Step3](./assets/3.png)

After installing, Follow:
Plugins ->Add New -> Search “Woocommerce”
When searching finished, install Woocommerce.
![Step4](./assets/4.png)

After installing Woocommerce, you need to input store information first.
![Step5](./assets/5.png)

Next, you need to choose industry type, product type and business detail
![Step6](./assets/6.png)

![Step7](./assets/7.png)

![Step8](./assets/8.png)

Final, you can choose the theme of the shop.
![Step9](./assets/9.png)

Now, your woocommerce finished setting. You can use woocommerce in the wordpress
![Step10](./assets/10.png)

The first steps are set up product in the wordpress.
![Step11](./assets/11.png)

First, you need to add a new product to wordpress. Find Products -> Add New to add a new product
![Step12](./assets/12.png)
You can input the product name, product description and the product prize. Also, you can upload a photo about the product. When edit finish, kick Publish.
![Step13](./assets/13.png)

You can kick Products -> All Products to verify product create or not.

Now, you go to katacoda and launch mysql container to check the tables of woocommerce
`docker exec -it mysql bash`{{execute}}

You should login mysql database server by using wordpress account
`mysql -u wordpress -p`{{execute}}

After that, input 12345 to be a password of  wordpress account.

You need to type show databases to show what kind of database in mysql.
`show databases;`{{execute}}

After that, you should use wordpress database to check the plugin log.
`use wordpress;`{{execute}}

Now, you can see all of the tables in the wordpress databases.
`show full tables;`{{execute}}

Now, you can execute the following SQL to verify the product in the database or not.
`select * from wp_wc_product_meta_lookup;`{{execute}}
The results show that this product in the database. It is because the product id of T-shirt1 is 11.


Now, back to wordpress to do the second steps. The second steps are set up payments in the wordpress
![Step14](./assets/14.png)

In the home press press Set up payments.
![Step15](./assets/15.png)
![Step16](./assets/16.png)
You need to install woocommerce payments plugin. After that, you can set up woocommerce payments account

![Step17](./assets/17.png)
You can go to WooCommerce -> Setting -> payments to enable or not payment method.

The third steps are set up marketing tools.
![Step18](./assets/18.png)
Marketing tools can help you to analyze business in the wordpress.

Now, we can start the hypothetical scenario of user buy product.
![Step19](./assets/19.png)
First, user can login our webpage to buy our product. User can go to Shop to select product. After that, it can add to cart.
![Step20](./assets/20.png)
Second, user can go to Cart to checkout product.
![Step21](./assets/21.png)
Final, user should input his/her personal information and choose the payment method. When the details input finished, user can place order.
![Step22](./assets/22.png)
You can make an order in the checkout page. This picture show that the order is received.

Now, you go to katacoda to verify the order in the database or not.
`select * from wp_wc_order_product_lookup;`{{execute}}

The results show that the order in the database. It is because the order Id is matching the order Id in the wordpress page.

Now, try another SQL
`select * from wp_woocommerce_order_items;`{{execute}}
Table wp_wc_order_product_lookup will show the general information of the order. Table wp_woocommerce_order_items will show the order item in what kind of order id.




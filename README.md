Task:
Your task is to set up an automated deployment process for a WordPress website
using Nginx as the web server, LEMP (Linux, Nginx, MySQL, PHP) stack, and GitHub
Actions as the CI/CD automation tool. The deployment process should follow security
best practices and ensure optimal performance of the website.

I am including below the step-by-step process that I followed to complete the above task.

Step 1: Launch an EC2 server. 
I have used an Ubuntu 22.04 machine with a t2 micro instance type having a private key for authentication along with firewall settings (Allowing SSH, HTTP, and HTTPS in the security group) and used free volume.

After successfully launching an instance, access via ssh. 

I am providing the output that I got after performing step 1.

Output:

<img width="427" alt="image1" src="https://github.com/rinkgithub/assignment/assets/130461521/bf87d0ff-ab08-4506-a64b-25a6d80187ea">


Step 2: Update & Upgrade the packages.

sudo apt update

Output:

<img width="498" alt="image2" src="https://github.com/rinkgithub/assignment/assets/130461521/5e75f56f-fc40-4185-b0d3-869c66a872b0">

sudo apt upgrade -y

Output:

<img width="480" alt="image3" src="https://github.com/rinkgithub/assignment/assets/130461521/f15b4c0c-40eb-4838-96b4-2f84c61024a5">

Step 3: Install and Configure Nginx, MySQL/MariaDB, and PHP.

Install and Configure Nginx

sudo apt install nginx

Output:

<img width="483" alt="image4" src="https://github.com/rinkgithub/assignment/assets/130461521/9114e5a4-69ca-4bc9-84f1-1326d27898eb">

sudo systemctl start nginx

sudo systemctl enable nginx

Output:

<img width="499" alt="image5" src="https://github.com/rinkgithub/assignment/assets/130461521/40adb49f-4628-4358-b478-f7c171855a9b">

Install and Configure PHP

sudo apt install php-mysql php-gd php-common php-mbstring php-curl php-cli -y

sudo systemctl restart nginx

sudo apt install php-fpm -y

Install and Configure Mysql

sudo apt install mysql-server

Before going ahead, we need to configure the database so that we can use it with WordPress.

sudo mysql -u root

Output:

<img width="479" alt="image6" src="https://github.com/rinkgithub/assignment/assets/130461521/7bd79552-e57c-47a3-af75-bd28e3afe8cd">

ALTER USER 'root'@localhost IDENTIFIED WITH mysql_native_password BY 'Rinku123';

Output:

<img width="588" alt="image7" src="https://github.com/rinkgithub/assignment/assets/130461521/7fd71121-4a41-4e3e-9016-a8a0adc33c32">

CREATE USER 'rinku'@localhost IDENTIFIED BY 'Rinku123';

Output:

<img width="411" alt="image8" src="https://github.com/rinkgithub/assignment/assets/130461521/e2650123-50dd-4491-8e2c-9545613ed979">


 CREATE DATABASE Wordpress;

 Output:

 <img width="286" alt="image9" src="https://github.com/rinkgithub/assignment/assets/130461521/3929eb84-daf9-424c-99b9-71ecd917c4a4">


 GRANT ALL PRIVILEGES ON Wordpress.* TO 'rinku'@localhost;

 Output:

<img width="429" alt="image10" src="https://github.com/rinkgithub/assignment/assets/130461521/ac64171f-2e83-4dfe-b1da-012b6fa210f1">

Step 4: Download and Configure WordPress

1)	wget https://wordpress.org/latest.zip

Output:

<img width="922" alt="image11" src="https://github.com/rinkgithub/assignment/assets/130461521/12ff0a46-f19d-4036-a754-adcb337b052e">

2)	unzip latest.zip

Output:

<img width="320" alt="image12" src="https://github.com/rinkgithub/assignment/assets/130461521/84cd7190-16e1-4450-8a7c-bf9812eea34e">

 
3)	sudo mv wordpress/ /var/www/html
4)	sudo chown -R www-data:www-data /var/www/html
5)	cd /var/www/html

Output:

<img width="307" alt="image13" src="https://github.com/rinkgithub/assignment/assets/130461521/7bb4b946-c2b7-40ba-8532-9b20de8b1071">

Now we have to configure some settings in nginx server.
So, 
1) cd /var/www/html

Here we will get default folder. 

2) sudo cp default wordpress.conf

Now, change some configuration settings.

3) sudo vim wordpress.conf

After changing a few things. We can restart the nginx server.

4) sudo systemctl restart nginx

Output:

<img width="638" alt="image14" src="https://github.com/rinkgithub/assignment/assets/130461521/db6221ca-8b47-4a7b-a5f6-c44ee9f04671">

Logged in using credentials and got WordPress dashboard.

Output:

<img width="947" alt="image15" src="https://github.com/rinkgithub/assignment/assets/130461521/89db0f86-a3ef-4d99-82e1-de94d8a70547">

My sample website page on WordPress

Output:

<img width="775" alt="image16" src="https://github.com/rinkgithub/assignment/assets/130461521/aab75e0c-5ae0-41e6-ae2f-841863f93442">


Step 5: Now we have to secure the site so using Certbot.

1)	sudo apt install certbot python3-certbot-nginx
2)	sudo certbot –nginx

Output:

<img width="489" alt="image17" src="https://github.com/rinkgithub/assignment/assets/130461521/2cf2a1f4-9c3d-4874-ad4b-c574e3eeb093">

We need to mention the domain name and enter. Now we can test our domain name on the browser.

Note: We need to make sure that we have registered our domain name and created hosted zone or DNS name records. Route 53 can be used in order to create a hosted zone.

Also, some additional services can be used for better optimization of the server.
We can use an application load balancer and enable auto-scaling.

An Application Load Balancer is a type of load balancer provided by AWS. It is designed to distribute incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, and IP addresses, in order to improve the availability and fault tolerance of applications.

Auto Scaling is a feature provided by AWS that allows us to automatically adjust the number of EC2 instances in our application's fleet based on demand. The goal of Auto Scaling is to ensure that our application has the right amount of resources at any given time, helping us maintain a balance between performance, cost, and availability.


















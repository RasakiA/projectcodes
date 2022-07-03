## Project 2: LEMP STACK IMPLEMENTATION

#### Step 1: Create AWS virtual server 

#### Step 2: 
- update the servers package index using the apt update 
- install the nginx server web server 
- Verify the ngix server is up and running
- Open port 80 to receive any traffice from the web server
- As we know, we have TCP port 22 open by default on our EC2 machine to access it via SSH, so we need to add a rule to EC2 configuration to open inbound connection through port 80:

```bash
#update a list of packages in package manager
sudo apt update

#run nginx pakage installation
sudo apt install nginx

#check the status of the nginx web server if running appropriately
sudo systemctl status ngix

```

<!-- Images -->

![.](images/img_1.png)

![.](images/img_2.png)

![.](images/img_3.png)

![.](images/img_4.png)

![.](images/img_5.png)

- Process for opening port 80

![.](images/OpenPort80.gif)

- NGINX web server accessible 
![.](images/img_6.png)

#### Step 3: INSTALLING MYSQL
- Install mysql server 
- When prompted press Y and then enter 
- When installation is complete, log into mysql 


```bash
#use apt to acquire and install mysql server
sudo apt install msql-server

#log into mysql 
sudo mysql

#It’s recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system. Before running the script you will set a password for the root user, using mysql_native_password as default authentication method. We’re defining this user’s password as PassWord.1.
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';

#Exit mysql shell with 
exit 

```

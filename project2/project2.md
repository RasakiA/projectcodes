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

![.](images/OpenPort80.gif)

&nbsp;

#### Step 3: 
- Install mysql server 


```bash
#install mysql server
sudo apt install msql-server

#

```

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
- It’s recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system. Before running the script you will set a password for the root user, using mysql_native_password as default authentication method. We’re defining this user’s password as PassWord.1.

```bash
#use apt to acquire and install mysql server
sudo apt install msql-server

#log into mysql 
sudo mysql

#
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';

#Exit mysql shell with 
exit 

```

- Start the interactive script by running 

```bash 
sudo mysql_secure_installation

```

<p>This will ask if you want to configure the VALIDATE PASSWORD PLUGIN.

Note: Enabling this feature is something of a judgment call. If enabled, passwords which don’t match the specified criteria will be rejected by MySQL with an error. It is safe to leave validation disabled, but you should always use strong, unique passwords for database credentials.

Answer Y for yes, or anything else to continue without enabling.</p>

- Test if you’re able to log in to the MySQL console by typing:

```bash 
sudo mysql -p

exit
```

#### Step 4: INSTALLING PHP
- Install two packages at once with a single line of code
- You have Nginx installed to serve your content and MySQL installed to store and manage your data. Now you can install PHP to process code and generate dynamic content for the web server.
```bash 
#installing the PHP fastCGI process manager”, and tell Nginx to pass PHP requests to this software for processing

#Additionally, you’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases

sudo apt install pho-fpm php-mysql

```

#### Step 4: CONFIGURING NGINX TO USE PHP PROCESSOR
- Creating the root web directory for your_domain as follows: 
 
```bash 
#make the project folder directory
sudo mkdir /var/www/projectLEMP

```

- Next, assign ownership of the directory with the $USER environment variable, which will reference your current system user:
```bash 
#
sudo chown -R $USER:$USER /var/www/projectLEMP
```

- Then, open a new configuration file in Nginx’s sites-available directory using your preferred command-line editor. Here, we’ll use nano:
```bash 
#
sudo nano /etc/nginx/sites-available/projectLEMP
```

- This will create a new blank file. Paste in the following bare-bones configuration:
```bash 
#/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}
```

##### Here’s what each of these directives and location blocks do:

- listen — Defines what port Nginx will listen on. In this case, it will listen on port 80, the default port for HTTP.
- root — Defines the document root where the files served by this website are stored.
- index — Defines in which order Nginx will prioritize index files for this website. It is a common practice to list index.html files with a higher precedence than index.php files to allow for quickly setting up a maintenance landing page in PHP applications. You can adjust these settings to better suit your application needs.
- server_name — Defines which domain names and/or IP addresses this server block should respond for. Point this directive to your server’s domain name or public IP address.
- location / — The first location block includes a try_files directive, which checks for the existence of files or directories matching a URI request. If Nginx cannot find the appropriate resource, it will return a 404 error.
- location ~ \.php$ — This location block handles the actual PHP processing by pointing Nginx to the fastcgi-php.conf configuration file and the php7.4-fpm.sock file, which declares what socket is associated with php-fpm.
- location ~ /\.ht — The last location block deals with .htaccess files, which Nginx does not process. By adding the deny all directive, if any .htaccess files happen to find their way into the document root ,they will not be served to visitors.

- When you’re done editing, save and close the file. If you’re using nano, you can do so by typing CTRL+X and then y and ENTER to confirm.

- Activate your configuration by linking to the config file from Nginx’s sites-enabled directory:
```bash 
#
sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/
```

- This will tell Nginx to use the configuration next time it is reloaded. You can test your configuration for syntax errors by typing:
```bash 
#
sudo nginx -t
```

- You shall see following message:
```bash 
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

![.](images/img_xpng)

- If any errors are reported, go back to your configuration file to review its contents before continuing.
- We also need to disable default Nginx host that is currently configured to listen on port 80, for this run:

```bash 
#
sudo unlink /etc/nginx/sites-enabled/default
```

- When you are ready, reload Nginx to apply the changes:
```bash 
#
sudo systemctl reload nginx
```

- Your new website is now active, but the web root /var/www/projectLEMP is still empty. Create an index.html file in that location so that we can test that your new server block works as expected:
```bash 
#
sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html
```

- Now go to your browser and try to open your website URL using IP address:
```bash 
#
http://<Public-IP-Address>:80
```

<p>If you see the text from ‘echo’ command you wrote to index.html file, then it means your Nginx site is working as expected.
In the output you will see your server’s public hostname (DNS name) and public IP address. You can also access your website in your browser by public DNS name, not only by IP – try it out, the result must be the same (port is optional)</p>

```bash 
http://<Public-DNS-Name>:80
```

<p>You can leave this file in place as a temporary landing page for your application until you set up an index.php file to replace it. Once you do that, remember to remove or rename the index.html file from your document root, as it would take precedence over an index.php file by default. </p>

<p>Your LEMP stack is now fully configured. In the next step, we’ll create a PHP script to test that Nginx is in fact able to handle .php files within your newly configured website.</p>

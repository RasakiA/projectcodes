## LAMP STACK IMPLEMETATION

### Step 1 



### Step 2
<p>Install apache using ubuntu package manager 'apt':</p>

<!-- Code Blocks -->

```bash
  #update a list of packages in package manager
  sudo apt update
  
  #Run apache2 package installation
  sudo apt install apache2
```

<!-- Images -->

![Markdown Logo](https://www.markdown-here.com/img/icon256.png)


<p>To verify that apache2 is running as a Service in our OS, use following command</p>

```bash
  #check the status of the apache2 server on the node
  sudo systemctl status apache2  
```
<!-- Images -->

![Markdown Logo](https://www.markdown-here.com/img/icon256.png)


<p>If it is green and running, then you did everything correctly – you have just launched your first Web Server in the Clouds!</p>


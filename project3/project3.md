## MERN STACK IMPLEMENTATION

#### SIMPLE TO-DO APPLICATION ON MERN WEB STACK

##### In this project, you are tasked to implement a web solution based on MERN stack in AWS Cloud.

##### MERN Web stack consists of following components:

##### MongoDB: A document-based, No-SQL database used to store application data in a form of documents.

##### ExpressJS: A server side Web Application framework for Node.js.

##### ReactJS: A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components.

##### Node.js: A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser.


<p>As shown on the illustration above, a user interacts with the ReactJS UI components at the application front-end residing in the browser. This frontend is served by the application backend residing in a server, through ExpressJS running on top of NodeJS.</p>

<p>Any interaction that causes a data change request is sent to the NodeJS based Express server, which grabs data from the MongoDB database if required, and returns the data to the frontend of the application, which is then presented to the user.</p>

#### STEP 1 – BACKEND CONFIGURATION

Update ubuntu

`````bash 
sudo apt update 
`````
&nbsp;

Upgrade Ubuntu

`````bash 
sudo apt upgrade
`````
&nbsp;

Lets get the location of Node.js software from Ubuntu repositories.

`````bash 
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
`````
&nbsp;

Install Node.js on the server
Install Node.js with the command below
`````bash
sudo apt-get install -y nodejs
`````

&nbsp;

<p>Note: The command above installs both nodejs and npm. NPM is a package manager for Node like apt for Ubuntu, it is used to install Node modules & packages and to manage dependency conflicts.</p>

Verify the node installation with the command below

`````bash 
node -v 
`````
&nbsp;

Verify the node installation with the command below
`````bash 
npm -v 
`````

&nbsp;

Application Code Setup
Create a new directory for your To-Do project:
`````bash 
mkdir Todo
`````

&nbso;

Run the command below to verify that the Todo directory is created with ls command
`````bash
ls
`````
&nbsp;

Now change your current directory to the newly created one:
`````bash
cd Todo
`````
&nbsp;

Next, you will use the command npm init to initialise your project, so that a new file named package.json will be created. This file will normally contain information about your application and the dependencies that it needs to run. Follow the prompts after running the command. You can press Enter several times to accept default values, then accept to write out the package.json file by typing yes.

`````bash
npm init
`````

&nbsp;

- Run the command ls to confirm that you have package.json file created.



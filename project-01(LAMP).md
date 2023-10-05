#  WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS

***

#### 1. A technology stack is a collection of frameworks and tools used in the creation of a software product. This collection of frameworks and technologies has been carefully selected to operate together to create a well-functioning program. They are abbreviations for individual techno


#### 2. AWS account setup and provisioning of an Ubuntu Server



#### 3. Steps
1. Signed up for an AWS account.
2. Logged in as IAM user
3. In the VPC console, I create the Security Group
4. Launched an EC2 instance
5. I selected the Ubuntu free tier instance
6. I set the required configurations (Enabled public IP, security group, and key pair)

![Step 3 screenshot](<images/project01/Screenshot from 2023-10-04 22-39-18.png>)


#### 4.  INSTALLING APACHE AND UPDATING THE FIREWALL
 Steps


 1. Install Apache using Ubuntu’s package manager ‘apt', Run the following commands: To update a list of packages in package manager:
   ```
    sudo apt update
```
![Step 5 screenshot](<images/project01/Screenshot from 2023-10-04 22-39-36.png>)


 2. To run apache2 package installation:
```
    sudo apt install apache2
```

![step 5.1 screenshot](<images/project01/Screenshot from 2023-10-04 22-41-47.png>)


3. Next, verify that Apache2 is running as a service in the OS. run:
```
    sudo systemctl status apache2
```
4. The green light indicates Apache2 is running.
![Step 6 screenshot](<images/project01/Screenshot from 2023-10-04 22-42-01.png>)


 6. Open port 80 on the Ubuntu instance to allow access from the internet.
7. Access the Apache2 service locally in our Ubuntu shell by running: 
**ip address of your insance** or **curl http://localhost:80** or **curl http://127.0.0.1:80** This command would output the Apache2 payload indicating that it is access
![Step 7 screenshot](<images/project01/Screenshot from 2023-10-04 22-43-25.png>)


#### 5. INSTALLING MYSQL
Steps
In this step, I install a Database Management System (DBMS) to be able to store and manage data for the site in a relational database.


 1. Run ‘apt’ to acquire and install this software, run:
```
 sudo apt install mysql-server
```
2. Confirm installation by typing Y when prompted.

![Step 9 screenshot](<images/project01/Screenshot from 2023-10-04 22-48-51.png>)


 3. Once installation is complete, log in to the MySQL console by running: 
```
sudo mysql
```
![Step 10 screenshot](<images/project01/Screenshot from 2023-10-04 23-00-05.png>)


 4. Next, run a security script that comes pre-installed with MySQL, to remove some insecure default settings and lock down access to your database system. run: 


 
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password1';
```
![Step 12 screenshot](<images/project01/Screenshot from 2023-10-04 23-00-16.png>)


 5. Run the interactive script by typing:
```
 sudo mysql_secure_installation
```
and following the instructions.
6. Next, test that login to MySQL console works. Run: 
```
sudo mysql -p
```

 7. Type exit and enter to exit the console.


#### 6. INSTALLING PHP
Steps
1. To install these 3 packages at once, run:
```
sudo apt install php libapache2-mod-php php-mysql
```
![Step 13 & 14 screenshot](<images/project01/Screenshot from 2023-10-04 23-00-05.png>)


 2. After installation is done, run the following command to confirm your PHP version: **php -v**
![Step 15 screenshot](<images/project01/Screenshot from 2023-10-04 23-01-03.png>)


 3. At this point, your LAMP stack is completely installed and fully operational.



#### 7.   CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE
 Steps
1. Setting up a domain called projectlamp. Create the directory for projectlamp using ‘mkdir’. Run:
```
 sudo mkdir /var/www/projectlamp
```

![Step 16-18 screenshot](<images/project01/Screenshot from 2023-10-04 23-11-42.png>)


 2. assign ownership of the directory with your current system user, run:
``` sudo chown -R $USER:$USER /var/www/projectlamp
```


 3. Next, create and open a new configuration file in Apache’s sites-available directory. Type: sudo vi /etc/apache2/sites-available/projectlamp.conf


 4. This will create a new blank file. Paste in the following bare-bones configuration by hitting on I on the keyboard to enter the insert mode, and paste the text:



 ```
<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
</VirtualHost>
```


![Step 18 screenshot](<images/project01/Screenshot from 2023-10-04 23-05-18.png>)


5. To save and close the file. Hit the esc button on the keyboard, Type Type:wq w for write and q for quit and Hit ENTER to save the file.


 6. use the ls command to show the new file in the sites-available directory:
 ```
    sudo ls /etc/apache2/sites-available
```

7. Next, use a2ensite command to enable the new virtual host:
 ```
    sudo a2ensite projectlamp
```

 8. Reload Apache so these changes take effect: 
```
   $ sudo systemctl reload apache2
```
![Step 19-23 screenshot](<images/project01/Screenshot from 2023-10-04 23-11-42.png>)


![Step 19-23 screenshot](<images/project01/Screenshot from 2023-10-04 23-11-30.png>)




 9. Finally, reload Apache so these changes take effect: 
```
 $ sudo systemctl reload apache2


 10. Next, use a2ensite command to enable the new virtual host:
 ```
  $ sudo a2ensite projectlamp
```

 11. Disable the default website that comes installed with Apache. type:
```
   $ sudo a2dissite 000-default
```

12. Ensure your configuration file doesn’t contain syntax errors, run: 
```
    sudo apache2ctl configtest
```

13. Finally, reload Apache so these changes take effect: 
```
    sudo systemctl reload apache2
```

  14. The website is active, but the webroot/var/www/projectlamp is still empty. Create an index.html file in that location so that we can test that the virtual host works as expected:

* Type and run :

```
 sudo vi /var/www/projectlamp/index.html
```

see my input :
create a simple html page

 14. The website is active, but the webroot/var/www/projectlamp is still empty. Create an index.html file in that location so that we can test that the virtual host works as expected:

* Type and run :




```
    sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html
```


 15. Reload the public IP to see changes to the apache2 default page.

![Step 19-23 screenshot](<images/project01/Screenshot from 2023-10-04 23-11-52.png>)


#### 8.   ENABLE PHP ON THE WEBSITE
 Steps
```
1. With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php file. To make index.php file take precedence, we need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive.
```


 This is useful for setting up maintenance pages in PHP applications, by creating a temporary index.html file containing an informative message to visitors. Because this page will take precedence over the index.php page, it will then become the landing page for the application. 

```
Once maintenance is over, the index.html is renamed or removed from the document root, bringing back the regular application page.
```


 2. In case you want to change this behavior, you’ll need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive:

```
   sudo vim /etc/apache2/mods-enabled/dir.conf
```



<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>

![Step 39 screenshot](https://images.tango.us/workflows/f5bb192a-e935-4faa-bce3-6f7ee92f44ee/steps/07b3454d-f5e7-4c62-80cd-8965af15e804/1bf3dacd-0f53-4449-ab7b-6193b9c105ae.jpeg?crop=focalpoint&fit=crop&fp-x=0.5000&fp-y=0.5000&fp-z=1.0000&w=1200&mark-w=0.2&mark-pad=0&mark64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmsucG5n&ar=1363%3A549)


3. After saving and closing the file, you will need to reload Apache so the changes take effect:

```
 sudo systemctl reload apache2
```



4.  Finally, we will create a PHP Script to test if the PHP is correctly installed and configured on our Server.
 Now that we have a custom location to host our website's files and folders, 


5. we'll create a PHP test script to confirm that Apache is able to handle and process requests for PHP files.
* Create a new file named index.php inside our custom web root folder:

```
 vim /var/www/projectlamp/index.php
```


6. This will open a blank file. Add the following text, which is valid PHP code, inside the file:

```
<?php
phpinfo();
```
![Step 43 screenshot](https://images.tango.us/workflows/f5bb192a-e935-4faa-bce3-6f7ee92f44ee/steps/9fb10c6e-b9c3-4dc4-a60b-c23d2b8c13c9/3d18db69-f46d-47f1-b386-f262898effcf.jpeg?crop=focalpoint&fit=crop&fp-x=0.5000&fp-y=0.5000&fp-z=1.0000&w=1200&mark-w=0.2&mark-pad=0&mark64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmsucG5n&ar=1366%3A560)


7.  Save and close the file, then refresh the page to see changes.
![Step 44 screenshot](https://images.tango.us/workflows/f5bb192a-e935-4faa-bce3-6f7ee92f44ee/steps/c17cfd4f-2e40-4784-98b4-60ad29f416b9/117560c7-8089-4f5f-9883-89027590cd6f.jpeg?crop=focalpoint&fit=crop&fp-x=0.5000&fp-y=0.5000&fp-z=1.0000&w=1200&mark-w=0.2&mark-pad=0&mark64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmsucG5n&ar=1365%3A696)


8.  This page provides information about your server from the perspective of PHP. It is useful for debugging and ensuring that your settings are being applied correctly.


9.  If you can see this page in your browser, then your PHP installation is working as expected.


10.  After checking the relevant information about your PHP server through that page, it’s best to remove the file you created as it contains sensitive information about your PHP environment -and your Ubuntu server. You can use rm to do so:

\`\`\`

sudo rm /var/www/projectlamp/index

\`\`\`


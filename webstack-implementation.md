
## WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS

As you kick off your career in DevOps, you will soon realise that everything you will be doing as a DevOps engineer is around 
software, websites, applications etc.

And, there are different stack of technologies that make different solutions possible. These stack of technologies are regarded as
WEB STACKS.

Examples of Web Stacks include LAMP, LEMP, MEAN, and MERN stacks. 

As you proceed in your journey, you will be required to understand and implement all of these technology stacks. Lets have a short
close up on what a Technology stack is.

What is a Technology stack?
A technology stack is a set of frameworks and tools used to develop a software product. 
This set of frameworks and tools are very specifically chosen to work together in creating a well-functioning software. 
They are acronymns for individual technologies used together for a specific technology product. some examples are…

LAMP (Linux, Apache, MySQL, PHP or Python, or Perl)
LEMP (Linux, Nginx, MySQL, PHP or Python, or Perl)
MERN (MongoDB, ExpressJS, ReactJS, NodeJS)

After completing this lab, you will be able to achieve the following.

1. Become very confident on the Linux Terminal

2. Deepen your understanding of Web Stacks and familiarity between the differences between the different Web Technology stacks
such as LAMP, LEMP, MEAN, and MERN stacks
3. Have Solid Linux administration skills in Storage management, NFS, troubleshooting, and basic networking.

4. Basic knowledge of AWS platform and components used to host a Website of various Web stacks.

### AWS account setup and provisioning an Ubuntu Server
#### Steps
1. Signed up for an AWS account.
2. Logged in as IAM user
3. In the VPC console, I create Security Group
<img width="1433" alt="Screen Shot 2022-11-09 at 13 12 32" src="https://user-images.githubusercontent.com/39014215/200827705-f628b90d-6b82-499c-a0ed-fa7c0794db99.png">
4. Launched an EC2 instance
5.I selelected the Ubuntu free tier instance
6.I set the required configurations (Enabled public IP, security group, and key pair) and finally launched the instance.

<img width="1433" alt="Screen Shot 2022-11-09 at 13 12 32" src="https://user-images.githubusercontent.com/39014215/200828977-6d24cb76-afb1-4b9b-ac9f-c054d7bed3d8.png">

7. Next I SSH into the instance using Windows Terminal

8. In the Terminal, I typed cd Downloads to navigate to the location of my key-pair.

9. Inside the Downloads directory, I connect to my instance using its Public DNS.
<img width="1419" alt="Screen Shot 2022-11-09 at 13 33 39" src="https://user-images.githubusercontent.com/39014215/200831496-65928b45-7045-4de4-b3db-66f81d005b81.png">

### STEP 1 -INSTALLING APACHE AND UPDATING THE FIREWALL
#### Steps
1. Install Apache using Ubuntu’s package manager ‘apt', Run the following commands: To update a list of packages in package manager:
**sudo apt update**
<img width="1419" alt="Screen Shot 2022-11-09 at 13 38 03" src="https://user-images.githubusercontent.com/39014215/200832408-0fbdb12c-970f-4a0d-a164-e70aa7787f13.png">

2. To run apache2 package installation: sudo apt install apache2

3. Next, verify that Apache2 is running as a service in the OS. run: sudo systemctl status apache2

4. The green light indicates Apache2 is running.
5. <img width="1420" alt="Screen Shot 2022-11-09 at 13 41 11" src="https://user-images.githubusercontent.com/39014215/200833051-02d3a5a9-f419-4b79-ac2f-d75e5fe791c2.png">
6. Open port 80 on the Ubuntu instance to allow access from the internet.

7. Access the Apache2 service locally in our Ubuntu shell by running: curl http://localhost:80 or curl http://127.0.0.1:80 This command would output the Apache2 payload indicating that it is accessible locally in the Ubuntu shell.

8. Next, test that Apache HTTP server can respond to requests from the Internet. Open a browser and type the public IP of the Ubutun instance: http://54.197.194.49/:80 This outputs the Apache2 default page.
<img width="1427" alt="Screen Shot 2022-11-09 at 13 47 24" src="https://user-images.githubusercontent.com/39014215/200834387-40fbd526-8b97-42c7-8dd5-8c1171524dcf.png">

### STEP 2 -INSTALLING MYSQL
#### Steps
In this step, I install a Database Management System (DBMS) to be able to store and manage data for the site in a relational database.
1. Run ‘apt’ to acquire and install this software, run: **sudo apt install mysql-server**
2. Confirm intallation by typing Y when prompted.
3. Once installation is complete, log in to the MySQL console by running: **sudo mysql**
<img width="1420" alt="Screen Shot 2022-11-09 at 13 54 01" src="https://user-images.githubusercontent.com/39014215/200835708-22e428ef-5868-4e61-bedb-7a7c4da40adc.png">
4. Next, run a security script that comes pre-installed with MySQL, to remove some insecure default settings and lock down access to your database system. run: 
**ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';** then exit MySQL shell by typing exit and enter.
5. Run interactive script by typing: **sudo mysql_secure_installation** and following the instrustions.
6. Next, test that login to MySQL console works. Run: **sudo mysql -p** 
<img width="1422" alt="Screen Shot 2022-11-09 at 14 03 33" src="https://user-images.githubusercontent.com/39014215/200837715-148b78c3-cf67-40bb-9950-f1ad1940c207.png">
7. Type exit and enter to exit console.

### STEP 3 — INSTALLING PHP
#### Steps
1. To install these 3 packages at once, run:
**sudo apt install php libapache2-mod-php php-mysql**
<img width="1417" alt="Screen Shot 2022-11-09 at 14 08 40" src="https://user-images.githubusercontent.com/39014215/200838737-e93e31a2-464e-4344-a0c5-3dbcb57ce497.png">
2. After installation is done, run the following command to confirm your PHP version: **php -v**
<img width="1434" alt="Screen Shot 2022-11-09 at 14 10 13" src="https://user-images.githubusercontent.com/39014215/200839060-c446ccb9-5d8f-4a44-a994-785b95b6b969.png">
3. At this point, your LAMP stack is completely installed and fully operational.

### STEP 4 — CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE
#### Steps
1. Setting up a domain called projectlamp. Create the directory for projectlamp using ‘mkdir’. Run: **sudo mkdir /var/www/projectlamp**
2. assign ownership of the directory with your current system user, run: **sudo chown -R $USER:$USER /var/www/projectlamp**
3. Next, create and open a new configuration file in Apache’s sites-available directory. Tpye: **sudo vi /etc/apache2/sites-available/projectlamp.conf**
4. This will create a new blank file. Paste in the following bare-bones configuration by hitting on i on the keyboard to enter the insert mode, and paste the text:
**<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
  </VirtualHost>**
  
  5.To save and close the file. Hit the esc button on the keyboard, Type :, Type wq. w for write and q for quit and Hit ENTER to save the file.
  6. use the ls command to show the new file in the sites-available directory: **sudo ls /etc/apache2/sites-available**
  <img width="1440" alt="Screen Shot 2022-11-09 at 14 20 38" src="https://user-images.githubusercontent.com/39014215/200841074-9006b0ff-aaeb-4872-9c33-d400a07e4d86.png">
  7. Next, use a2ensite command to enable the new virtual host: **sudo a2ensite projectlamp**
  8. Disable the default website that comes installed with Apache. type: **sudo a2dissite 000-default**
  9. Esure your configuration file doesn’t contain syntax errors, run: **sudo apache2ctl configtest**
  10. Finally, reload Apache so these changes take effect: **sudo systemctl reload apache2**
  11. <img width="1435" alt="Screen Shot 2022-11-09 at 14 24 11" src="https://user-images.githubusercontent.com/39014215/200841761-110f8518-fb56-424e-b3eb-ba13b397ce3b.png">
  12. The website is active, but the web root /var/www/projectlamp is still empty. Create an index.html file in that location so that we can test that the virtual host works as expected:
**sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html**
<img width="1435" alt="Screen Shot 2022-11-09 at 14 24 11" src="https://user-images.githubusercontent.com/39014215/200842557-4864ac9f-6ca2-477c-a707-9cebb9d19680.png">

### STEP 5 — ENABLE PHP ON THE WEBSITE
#### Steps
1. With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php file. To make index.php file tak precedence need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive.
2. Run: **sudo vim /etc/apache2/mods-enabled/dir.conf** then:
**<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>**
4. Save and close file. using command :wq
5. Next, reload Apache so the changes take effect, type: **sudo systemctl reload apache2**
6. Finally, we will create a PHP script to test that PHP is correctly installed and configured on your server. Create a new file named index.php inside the custom web root folder, run: **vim /var/www/projectlamp/index.php**
7. This will open a blank file. Add the PHP code: 
**<?php
phpinfo();**
8. Save and close the file,using command :wq then refresh the page to see changes.
9. <img width="1427" alt="Screen Shot 2022-11-09 at 14 42 06" src="https://user-images.githubusercontent.com/39014215/200845678-b6e062d2-82b0-4942-b8fc-1ba4f9102182.png">

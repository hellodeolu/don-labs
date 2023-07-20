# What we’re learning about this week;
- AWS &
- Network

- Week 4 Walkthrough ([YouTube Week 4](https://bit.ly/wk4-Walkthrough))

**Contents** <a name="Contents"></a>
<!-- TOC -->
  * [What we’re learning about this week](#What-we’re-learning-about-this-week)
  * [RESOURCES](#RESOURCES)
    * [AWS](#AWS)
    * [Network](#Network)
  * [HANDS-ON PROJECTS](#HANDS-ON-PROJECTS)
  * [Back to Contents](#Contents)
<!-- TOC -->

# RESOURCES
I highly recommend engaging in a comprehensive learning approach. Start by watching at least one tutorial video from each subject, carefully assessing their content. Select the tutorial that resonates most with your learning preferences and embark on completing its hands-on projects. Additionally, I encourage you to utilize any spare time to enrich your knowledge further by delving into a book or informative doc. related to the subjects you are exploring. This well-rounded learning strategy will undoubtedly enhance your understanding and proficiency. 

Lastly, ensure a disciplined commitment to completing all assigned hands-on projects by the end of each week. By adhering to this diligent practice, you will reinforce your learning, gain practical experience, and foster a deeper understanding of the subject matter.

## AWS
### videos;
- AWS Tutorial For Beginners | AWS Full Course - Learn AWS In 10 Hours | AWS Training ([Edureka](https://www.youtube.com/watch?v=k1RI5locZE4))
- AWS Certified Cloud Practitioner Certification Course (CLF-C01) - Pass the Exam! ([freeCodeCamp](https://www.youtube.com/watch?v=SOTamWNgDKc))
- Amazon Web Services YouTube ([Amazon Web Services](https://www.youtube.com/user/AmazonWebServices/Cloud))


### others;
- Welcome to AWS Documentation ([AWS docs](https://docs.aws.amazon.com/))
- github awsdocs ([awsdocs](https://github.com/awsdocs))
- github aws-solutions ([aws-solutions](https://github.com/aws-solutions))
- github aws-samples ([aws-samples](https://github.com/aws-samples))
- github awslabs ([awslabs](https://github.com/awslabs))


## network
### tutorial videos
- DevOps - Networking knowledge base ([DevOps knowledge base](https://www.youtube.com/playlist?list=PL-dQ102CNNabGpUi1oMVI85c_aGaeac7H))
- Networking Tutorial for Beginners || Computer Networking Full Course by Network Engineer ([Network Kings](https://www.youtube.com/watch?v=0uflG0SemyM))
- Network Fundamentals ([Network Direction](https://www.youtube.com/playlist?list=PLDQaRcbiSnqF5U8ffMgZzS7fq1rHUI3Q8))

### books
- Linux Networking Cookbook-O'Reilly Media (2007) by Carla Schroder


# HANDS-ON PROJECTS

## Task 1 - Launch a static website on Amazon S3
- All you need to complete this task ([AWS doc](https://docs.aws.amazon.com/AmazonS3/latest/userguide/website-hosting-custom-domain-walkthrough.html))

### Before you begin
### Step 1: Register a custom domain with Route 53
### Step 2: Create two buckets
### Step 3: Configure your root domain bucket for website hosting
### Step 4: Configure your subdomain bucket for website redirect
### Step 5: Configure logging for website traffic
### Step 6: Upload index and website content
### Step 7: Upload an error document
### Step 8: Edit S3 Block Public Access settings
### Step 9: Attach a bucket policy
### Step 10: Test your domain endpoint
### Step 11: Add alias records for your domain and subdomain
### Step 12: Test the website
### Speeding up your website with Amazon CloudFront
### Cleaning up your example resources

## Task 2 - Get started with Amazon EC2 Linux instances
- All you need to complete this task ([AWS doc](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html))

### step 1; Launch an instance

### step 2; Connect to your instance

### step 3; Clean up your instance

## Task 3 - LAMP_Stack_Implementation

Web stack implementation (lamp stack) in AWS
- LAMP stack (collection Linux, Apache, MySQL, PHP or Python, or Perl)
- LAMP is basically a collection of software that you require to create a dynamic website and web applications. These tools are capable enough that you don’t require any other tool for the purpose. LAMP tools are free and open-source.

**Steps** <a name="Steps"></a>
* [step 1; installing apache and updating the firewall](#installing_apache)
* [step 2; installing mysql](#installing_mysql)
* [step 3; installing php](#installing_php)
* [step 4; creating a virtual host for your website using apache](#virtual_host)
* [step 5; enable php on the website](#enable_php)

### installing_apache
- Update the repositries and install Apache using Ubuntu's package manager by running command:
```
sudo apt update 
sudo apt install apache2
```
- Verify that apache2 is running as a Service in the OS:
```
sudo systemctl status apache2
```
![screenshot_here](/docs/..)

- Requested Apache HTTP server on port 80:
```
curl http://localhost:80
```
- Verify if Apache HTTP server can respond to requests from the Internet; check screenshoot below

![screenshot_here](/docs/..)

### installing_mysql
- Install MySQL by running this command:
```
sudo apt install mysql-server
```
- Run a security script that comes pre-installed with MySQL:
```
sudo mysql_secure_installation
```
- Log into MySQL to test connection:
```
sudo mysql
```
- Then, exit from MySQL
``` 
mysql> exit
```
![screenshot_here](/docs/..)

### installing_php
- In addition to the php package, the server will need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases.
- libapache2-mod-php will be required to enable Apache to handle PHP files. Core PHP packages will automatically be installed as dependencies.
- All the 3 packages will be installed at once by running:
```
sudo apt install php libapache2-mod-php php-mysql
```
- confirmed my PHP version by running:
```
php -v
```

### virtual_host
- To test the setup with a PHP script, set up a Apache Virtual Host to hold the website’s files and folders - Objective is to setup a domain called ‘projectlamp’.
- Apache on Ubuntu has one server block enabled by default that is configured to serve documents from the /var/www/html directory.
- So, create a directory next to the default one with this command;
```
sudo mkdir /var/www/projectlamp
```
- Also, assign ownership of the directory;
```
sudo chown -R $USER:$USER /var/www/projectlamp
```
- Create virtual host configuration file in Apache’s sites-available directory;
```
sudo vim /etc/apache2/sites-available/projectlamp.conf
```
- In the editor, paste in the following configuration by hitting on i on the keyboard to enter the insert mode, and paste the text;
```
<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Saved and closed the file, as shown below:
1. Hit the esc button on the keyboard
2. Type :
3. Type wq! (w means write and q means quit)
4. Hit ENTER to save the file
- To show the new file in the sites-available directory
```
sudo ls /etc/apache2/sites-available
```
![screenshot_here](/docs/..)

- enable the new virtual host
```
sudo a2ensite projectlamp
```
- Disable the default website that comes installed with Apache. If this is not done Apache’s default configuration would overwrite the virtual host.
```
sudo a2dissite 000-default
```
- To make sure the configuration file doesn’t contain syntax errors;
```
sudo apache2ctl configtest
```
- Reload Apache so these changes take effect;
```
sudo systemctl reload apache2
```
- Create an index.html file in that location so that you can test that the virtual host works as expected - in /var/www/projectlamp/:
```
sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html
```
### note
- The >> redirection operator will append lines to the end of the specified file
- The > redirection operator will empty and overwritethe specified file

### enable_php
- With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php file. To change this behavior, need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive.
```
sudo vim /etc/apache2/mods-enabled/dir.conf
```
```
<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```
- Reload Apache so the changes take effect:
```
sudo systemctl reload apache2
```
- Create a PHP test script to confirm that Apache is able to handle and process requests for PHP files by opening a new file named index.php inside the custom web root folder:
```
vim /var/www/projectlamp/index.php
```
- Enter the code below inside the file
```
<?php
phpinfo();
```
- Refresh your EC2 public ip address url page
![screenshot_here](/docs/..)

- It’s best to remove the file you created as it contains sensitive information about your PHP environment -and your Ubuntu server.
```
sudo rm /var/www/projectlamp/index.php
```
### don't forget to clean resources on AWS after use!!!

Congratualation! 

[Back to Contents](#Contents)
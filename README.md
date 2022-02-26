# WebServerProject1

## To install Apache and create two sites we first have to go to the website.
 First, ensure that you have the latest C++ redistributable from visual studio and download this, choosing the 64 bit.
 Once this is downloaded, run and agree to the terms then install. After the set says succesful we move to the next step.
1. Go Here -> (https://www.apachelounge.com/download/#google_vignette) to download Apache 2.4.52 Win64.
2. Download the zip folder called  httpd-2.4.52-win64-VS16.zip and extract all.   
3. Copy folder called Apache24 onto your C: Drive. 
4. Open a Command prompt with admin privileges and cd into the Apache24 folder and go into bin by typing cd C:\Apache24\bin.
5. Then install the apache service by typing httpd.exe -k install.

![](screenshots/line11.PNG)

7. It will ask you for windows firewall access, click allow access.
8. To start it type in your terminal httpd.exe -k start.
9. After doing this, you can test your browser to see if it works. 
10. Go to localhost in your web browser and you should see a message saying, " It works!".
![itworks](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/itworks.PNG)
12. You can also shut down apache by pressing Cntrl+C.

## How to disable directory listing
1. Open notepad, right click and run ad administrator. 
2. go to C:\Apache24\conf\httpd.conf and opwn this file.
- Scroll down Mid-way of the file, you will see Options **Indexes FollowSymLinks**
- Change this to **Indexes FollowSymLinks** and save and close. 
![indexes](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/indexes.PNG)

## How to add two sites (vhosts)
1. To add 2 sites go to C:\Apache24\htdocs.
2. There you will see an index.html file which comes with htdocs.
3. Create two folders called site1.tbd and site2.tbd and add an index.html inside them both were you add your html/css information for your site.
- Site 1 
![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/site1tbd.PNG)
- Site 2
![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/site2-2.PNG)
5. To be able to implement and host multiple sites we would have to go to C:\Apache24\conf into our httpd.conf file.
- When there do a ctrl-f search for **#Include conf/extra/httpd-vhosts.conf**
- Once there you remove the # that is before **Include** this uncomments this line by moving the comment marker.
-Ctrl-s to save this. 
![includes](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/includes.PNG)
5. Go to C:\Apache24\conf\extra and open the httpd-vhosts.conf file and there you will see virtual host information and port information.
6. Enter the following for site 1 and site 2.
- Each of our individual sites that we want to publish is referred to as a virtual host.
![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/line28.PNG)
- Lastly, to resolve a name to an ip address go to C:\Windows\System32\drivers\etc.
- Click show all files to see your hosts file.
- Enter the ip address and site1.tbd
- Followed by the ip address and site2.tbd. 
![hostfile](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/hostlast.PNG)
- By doing this our client is able to resolve site1.tbd and site2.tbd to the ip of the local server.

## How to install PHP
1. First you need to download the PHP files
2. To do this you’ll need the PHP Windows installer. Get the latest PHP 8 x64 Thread Safe ZIP package from. 
3. ![](https://www.php.net/downloads.php) 
4. Extract the files
5. ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/phpextract.PNG)
6. Create a new php folder in the root of your **C:\** drive and extract the contents of the ZIP into it.
7. ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/phpdownload.PNG)
8. You can install PHP d anywhere on your system, but you’ll need to change the paths referenced below if C:\php isn’t used.
9. Now we add **C:\php** to the path environment variable
10. To ensure Windows can find the PHP executable, you need to change the PATH environment variable. 
11. Click the Windows Start button and type “environment”, then click Edit the system environment variables. 
12. Select the Advanced tab, and click the Environment Variables button.
13. Then scroll down the System variables list and click Path followed by the Edit button.
14. Click New and add C:\php:
![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/php1.PNG)
15. Click OK until you’re done. No need to reboot, it may be helpful to close and restart any cmd terminals you have open.
16. Configure PHP as an Apache module
17. Go to services to verfiy that apache isnt running, if it is running stop the service.
18. Open its **C:\Apache24\conf\httpd.conf** configuration file in a text editor.
19. Add the following lines to the bottom of the file to set PHP as an Apache module (change the file locations if necessary):

#### PHP8 module
PHPIniDir "C:/php"
LoadModule php_module **C:/php/php8apache2_4.dll.**
AddType application/x-httpd-php .php
![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/php2.PNG)

17. As an option, you change the DirectoryIndex setting to load index.php instead of index.html when it can be found. 
18. The current setting that you will see is:

<IfModule dir_module>
    DirectoryIndex index.html
</IfModule>

19. Change this to:
<IfModule dir_module>
    DirectoryIndex index.php index.html
</IfModule>
![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/php1.PNG)
![php4](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/php4.PNG)

20. Save your httpd.conf and test the updates in the command line by typing the following:

21. cd into **C:\Apache24\bin**
type: httpd -t
Syntax OK should appear … unless you have errors in your configuration.
If you didn't get an error you can continue by restarting Apache with httpd.

![php6](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/php6.PNG)

22. To confirm, test a PHP file by renaming index.html to index.php in Apache’s web page root folder at C:\Apache24\htdocs.
23. Add the following PHP code:

> <html>
> <body>
> <h1>This is Maya Pierre and this is site one, it works!</h1>
> <?php
> phpinfo();
> ?>
> </body>
> </html>

24. Go into **httpd.conf** file, Ctrl-f to search and ensure your <IfModule dir_module> has this:
 > <IfModule dir_module>
 >   DirectoryIndex index.php index.html
> </IfModule>
24. Now open a web browser and enter your server address: http://site1.tbd/. 
25. A PHP version of the previous page will appear showing the various PHP and Apache configuration settings.
![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/site1-1.PNG)
26. So you can now create PHP sites and applications in any sub-folder of C:\Apache24\htdocs.

 
## How to add SSL Certificates to one site
 
 
## How to install MySQL 
####To install MySQL on WindowsMySQL can be installed on 64-bit editions and require the following runtimes:
-.NET 4.5.2
-the Visual C++ redistributable

1. Create a folder on your C:\ drive called mysql to extract the contents of the ZIP to C:\mysql
2. Next create another folder where database data will be stored, for example as C:\mysqldata
3. Using a folder outside of C:\mysql is safer and allows you to upgrade application files.
4. ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/mysql1.PNG)
5. ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/mysql1.PNG)
6. Create a my.ini file in C:\mysql which specifies the application and data folders. for example:

-[mysqld]
#installation path
basedir=C:/mysql
#data directory
datadir=C:/mysqldata
7. Now we will initialize the data folder by creating a default root user without a password.
8. Entering the following command at the console prompt:

- C:\mysql\bin\mysqld.exe --initialize-insecure --user=mysql

![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/mysql3.PNG)

9. The server can now be started with:
- C:\mysql\bin\mysqld.exe --console
10. Use the MySQL client by entering C:\mysql\bin\mysql.exe -u root in another console. 
11. You can now issue SQL commands such as show databases; and quit by typing exit.
![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/mysql4.PNG)
12. The shut down the server we will type:
- C:\mysql\bin\mysqladmin.exe -u root shutdown
![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/mysql5.PNG)
- MySQL can also be installed as an auto-starting Windows service:
13. To do this, type  in the command prompt:
- C:\mysql\bin\mysqld.exe --install
![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/mysql7.PNG)
14. The service will launch on reboot or you can enter net start mysql to start it immediately. 
15. It can be stopped using net stop mysql or managed using the Services panel in Windows Administrative Tools.
![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/mysql6.PNG)
17. Lastly, you can have the service fully removed by typing:
- net stop mysql
- C:\mysql\bin\mysqld.exe --remove

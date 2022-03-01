# PHP INSTALLATION ON WINDOWS 10

Apache is a pre-requisite required for this walk through.
The PHP version used in this tutorial: PHP 8.1 (8.1.3)    
Referenced from: [How to Install PHP on Windows 10](https://www.sitepoint.com/how-to-install-php-on-windows/)

---

## TABLE OF CONTENTS
1. [DOWNLOAD AND EXTRACT THE FILES](#download-and-extract-the-files)
2. [CONFIGURE PATH TO ENVIRONMENT VARIABLE](#configure-path-to-environment-variable)
3. [PHP MODULE AND DEFAULT PHP FILE](#php-module-and-default-php-file)
4. [TEST](#test)

---

## DOWNLOAD AND EXTRACT THE FILES

1. First you need to download the PHP files.  
2. To do this you’ll need the PHP Windows installer. 
3. Get the latest PHP 8 x64 Thread Safe ZIP package from [HERE](https://www.php.net/downloads.php).    
4. Extract the files.  
> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/phpextract.PNG)  
5. Create a new php folder in the root of your **C:\** drive and extract the contents of the ZIP into it.  
> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/phpdownload.PNG)  
6. You can install PHP anywhere on your system.  
7. But you’ll need to change the paths referenced below if `C:\php` isn’t used.
---  

## CONFIGURE PATH TO ENVIRONMENT VARIABLE 
1. Now we add `C:\php` to the path environment variable.  
2. To ensure Windows can find the PHP executable, you need to change the PATH environment variable.  
3. Click the Windows Start button and type “environment”, then click Edit the system environment variables.  
4. Select the Advanced tab, and click the Environment Variables button.  
5. Then scroll down the System variables list and click Path followed by the Edit button.  
6. Click New and add `C:\php`:  
> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/php1.PNG)  
7. Click OK until you’re done. No need to reboot, it may be helpful to close and restart any cmd terminals you have open.
8. Configure PHP as an Apache module.  
9. Go to services to verfiy that apache isnt running, if it is running stop the service.
---

## PHP MODULE AND DEFAULT PHP FILE
1. Open its `C:\Apache24\conf\httpd.conf` configuration file in a text editor.
2. We now need to configure PHP as a PHP module.
3. Add the following lines to the bottom of the file to set PHP as an Apache module (change the file locations if necessary).  

```
> # PHP8 module  
> PHPIniDir C:/php  
> LoadModule php_module C:/php/php8apache2_4.dll
> AddType application/x-httpd-php .php  
```

> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/php2.PNG)  

4. As an option, you change the DirectoryIndex setting to load index.php instead of index.html when it can be found. 
5. The current setting that you will see is:  
```
> <IfModule dir_module>  
>    DirectoryIndex index.html  
> </IfModule>  
```
6. Change this to:
  
```
> <IfModule dir_module>  
>    DirectoryIndex index.php index.html  
> </IfModule>  
```

> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/php1.PNG)  
> ![php4](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/php4.PNG)  

7. Save your httpd.conf and test the updates in the command line by typing the following:  

8. cd into `C:\Apache24\bin`, type the following code:  
```
httpd -t
```
9. ***Syntax OK*** should appear unless you have errors in your configuration.  
- If you didn't get an error you can continue by restarting Apache with httpd.  
> ![php6](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/php6.PNG)  
---

## TEST
1. To confirm the configuration, test a PHP file by renaming index.html to index.php in Apache’s web page root folder at `C:\Apache24\htdocs`.  
2. Add the following PHP code or similar:    
```
> \<html>  
> \<body>  
> \<h1>This is Maya Pierre and this is site one, it works!</h1>  
> <?php  
> \phpinfo();  
> \?>  
> \</body>  
> \</html>  
```  
  
3. Go into `httpd.conf` file, Ctrl-f to search and ensure your `<IfModule dir_module>` has this:
```
 > <IfModule dir_module>
 >   DirectoryIndex index.php index.html
> </IfModule>
```

4. Now open a web browser and enter your server address: `http://site1.tbd/`.  
5. A PHP version of the previous page will appear showing the various PHP and Apache configuration settings.  
 
> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/site1-1.PNG)  
6. So you can now create PHP sites and applications in any sub-folder of `C:\Apache24\htdocs`.
---

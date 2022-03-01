
## How to install PHP
1. First you need to download the PHP files.  
2. To do this you’ll need the PHP Windows installer. 
3. Get the latest PHP 8 x64 Thread Safe ZIP package from [HERE](https://www.php.net/downloads.php).    
4. Extract the files.  
> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/phpextract.PNG)  
5. Create a new php folder in the root of your **C:\** drive and extract the contents of the ZIP into it.  
> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/phpdownload.PNG)  
6. You can install PHP anywhere on your system
7. But you’ll need to change the paths referenced below if `C:\php` isn’t used.  
10. Now we add `C:\php` to the path environment variable.  
11. To ensure Windows can find the PHP executable, you need to change the PATH environment variable.  
12. Click the Windows Start button and type “environment”, then click Edit the system environment variables.  
13. Select the Advanced tab, and click the Environment Variables button.  
14. Then scroll down the System variables list and click Path followed by the Edit button.  
15. Click New and add `C:\php`:  
> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/php1.PNG)  
16. Click OK until you’re done. No need to reboot, it may be helpful to close and restart any cmd terminals you have open.
17. Configure PHP as an Apache module.  
18. Go to services to verfiy that apache isnt running, if it is running stop the service.
19. Open its `C:\Apache24\conf\httpd.conf` configuration file in a text editor.
20. Add the following lines to the bottom of the file to set PHP as an Apache module (change the file locations if necessary)  
```
> \# PHP8 module  
> PHPIniDir C:/php  
> LoadModule php_module C:/php/php8apache2_4.dll
> AddType application/x-httpd-php .php  
```

> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/php2.PNG)  

20. As an option, you change the DirectoryIndex setting to load index.php instead of index.html when it can be found. 
21. The current setting that you will see is:  
```
> <IfModule dir_module>  
>    DirectoryIndex index.html  
> </IfModule>  
```
22. Change this to:
  
```
> <IfModule dir_module>  
>    DirectoryIndex index.php index.html  
> </IfModule>  
```

> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/php1.PNG)  
> ![php4](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/php4.PNG)  

23. Save your httpd.conf and test the updates in the command line by typing the following:  

24. cd into `C:\Apache24\bin`, type the following code:  
```
httpd -t
```
25. ***Syntax OK*** should appear unless you have errors in your configuration.  
- If you didn't get an error you can continue by restarting Apache with httpd.  
> ![php6](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/php6.PNG)  

26. To confirm, test a PHP file by renaming index.html to index.php in Apache’s web page root folder at C:\Apache24\htdocs.  
27. Add the following PHP code:  
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

28. Go into `httpd.conf` file, Ctrl-f to search and ensure your `<IfModule dir_module>` has this:
```
 > <IfModule dir_module>
 >   DirectoryIndex index.php index.html
> </IfModule>
```

29. Now open a web browser and enter your server address: `http://site1.tbd/`.  
30. A PHP version of the previous page will appear showing the various PHP and Apache configuration settings.  
> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/site1-1.PNG)  
31. So you can now create PHP sites and applications in any sub-folder of `C:\Apache24\htdocs`.

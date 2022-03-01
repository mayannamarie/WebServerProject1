# MYSQL INSTALLATION ON WINDOWS 10
**To install MySQL on WindowsMySQL can be installed on 64-bit editions and require the following runtimes:**

- .NET 4.5.2
- The Visual C++ redistributable
- Reference: [How to Install MySQL](MySQL version used in this tutorial: MySQL Community Server 8.0.28)
---
## Table of Contents
1. [DOWNLOAD AND EXTRACT](#download-and-extract)
2. [SPECIFYING FILE APPLICATION AND DATA FOLDERS](#specifying-file-application-and-data-folders)
3. [INITIALIZE DATA FOLDER AND CREATING ROOT USER](#initialize-data-folder-and-creating-root-user)
4. [CONFIGURE AND TEST MYSQL AS AUTO STARTING WINDOWS SERVICE](#configure-and-test-mysql-as-auto-starting-windows-service)
---

## DOWNLOAD AND EXTRACT 
1. Download the MySQL zip file from [here](https://dev.mysql.com/downloads/mysql/).
2. Create a folder on your `C:\` drive called mysql to extract the contents of the ZIP to `C:\mysql`.
3. Next create another folder where database data will be stored, for example as `C:\mysqldata`.
4. Using a folder outside of `C:\mysql` is safer.
5. This allows you to upgrade application files, see below.

> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/mysql1.PNG)  
> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/mysql1.PNG)  
---  

## SPECIFYING FILE APPLICATION AND DATA FOLDERS
1. Create a my.ini file in `C:\mysql` which specifies the application and data folders, for example:  

```
[mysqld]
#installation path
basedir=C:/mysql
#data directory
datadir=C:/mysqldata
```  
---  

## INITIALIZE DATA FOLDER AND CREATING ROOT USER  
1. Now we will initialize the data folder by creating a default root user without a password.  
2. Entering the following command at the console prompt:  

`C:\mysql\bin\mysqld.exe --initialize-insecure --user=mysql`  

> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/mysql3.PNG)  

3. The server can now be started with:
`C:\mysql\bin\mysqld.exe --console`  
4. Use the MySQL client by entering C:\mysql\bin\mysql.exe -u root in another console. 
5. You can now issue SQL commands such as show databases; and quit by typing exit.

> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/mysql4.PNG)  

6. The shut down the server we will type:
`C:\mysql\bin\mysqladmin.exe -u root shutdown`  

> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/mysql5.PNG)  
 ---  
 
 ## CONFIGURE AND TEST MYSQL AS AUTO STARTING WINDOWS SERVICE  
- ***MySQL can also be installed as an auto-starting Windows service:***  
1. To **test** this, type this in the command prompt:  
`C:\mysql\bin\mysqld.exe --install`  

> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/mysql7.PNG)  

2. The service will launch on reboot or you can enter net start mysql to start it immediately. 
3. It can be stopped using net stop mysql or managed using the Services panel in Windows Administrative Tools.  

> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/mysql6.PNG)  

4. Lastly, you can have the service fully removed by typing the following commands:  
```
net stop mysql
C:\mysql\bin\mysqld.exe --remove
```  
--- 

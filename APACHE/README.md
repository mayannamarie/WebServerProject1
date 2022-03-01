## To install Apache and create two sites we first have to go to the website.
 First, ensure that you have the latest C++ redistributable from visual studio and download this, choosing the 64 bit.
 Once this is downloaded, run and agree to the terms then install. After the set says succesful we move to the next step. 
 
 ## TABLE OF CONTENT
1. [DOWNLOAD THE APACHE FILES](#download-the-apache-files)  
2. [START APACHE](#start-apache)
4. [DISABLE DIRECTORY LISTING](#disable-directory-listing)
5. [CONFIGURE TWO SITES](#configure-two-sites)
6. [SSL CONFIGURATION ON ONE SITE](ssl-configuration-on-one-site)
 
 ## DOWNLOAD THE APACHE FILES
1. Download [Apache](https://www.apachelounge.com/download/#google_vignette) 2.4.52 Win64.
2. Download the zip folder called  httpd-2.4.52-win64-VS16.zip and extract all.   
3. Copy folder called Apache24 onto your C: Drive. 
4. Open a Command prompt with admin privileges and cd into the Apache24 folder and go into bin by typing cd C:\Apache24\bin.
5. Then install the apache service by typing httpd.exe -k install.  
> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/line11.PNG)

## START APACHE
1. It will ask you for windows firewall access, click allow access.
2. To start it type in your terminal httpd.exe -k start.
3. After doing this, you can test your browser to see if it works. 
4. Go to localhost in your web browser and you should see a message saying, " It works!".
> ![itworks](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/itworks.PNG)  
5. You can also shut down apache by pressing Ctrl+C.

## DISABLE DIRECTORY LISTING
1. Open notepad, right click and run ad administrator. 
2. go to C:\Apache24\conf\httpd.conf and opwn this file.
- Scroll down Mid-way of the file, you will see Options 
**Indexes FollowSymLinks**
- Change this to **Indexes FollowSymLinks** and save and close. 
> ![indexes](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/indexes.PNG)  

## CONFIGURE TWO SITES
1. To add 2 sites(vhosts) go to C:\Apache24\htdocs.
2. There you will see an index.html file which comes with htdocs.
3. Create two folders called site1.tbd and site2.tbd and add an index.html inside them both were you add your html/css information for your site.
- Site 1 
> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/site1tbd.PNG)  
- Site 2
![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/site2-2.PNG)  
4. To be able to implement and host multiple sites we would have to go to C:\Apache24\conf into our httpd.conf file.
- When there do a ctrl-f search for **#Include conf/extra/httpd-vhosts.conf**
- Once there you remove the # that is before **Include** this uncomments this line by moving the comment marker.
-Ctrl-s to save this. 
> ![includes](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/includes.PNG)  
5. Go to C:\Apache24\conf\extra and open the httpd-vhosts.conf file and there you will see virtual host information and port information.
6. Enter the following for site 1 and site 2.
- Each of our individual sites that we want to publish is referred to as a virtual host.
> ![](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/line28.PNG)  
7. Lastly, to resolve a name to an ip address go to C:\Windows\System32\drivers\etc.
- Click show all files to see your hosts file.
- Enter the ip address and site1.tbd
- Followed by the ip address and site2.tbd. 
> ![hostfile](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/hostlast.PNG)  
- By doing this our client is able to resolve site1.tbd and site2.tbd to the ip of the local server.

## SSL CONFIGURATION ON ONE SITE
 
1. Edit the `<VirtualHost *:80>` element of site2 as the following:  

 ```
 <VirtualHost *:80>  
	 ServerName site2.tbd  
  	 Redirect permanent / https://site2.tbd/  
	 DocumentRoot "${SRVROOT}/htdocs/site2.tbd/"  
 </VirtualHost>  
```
2. Open the `httpd.conf` file and uncomment the `ssl_module modules/mod_ssl.so` and `conf/extra/httpd-default.conf` modules.
3. Also in this same directory of httpd.conf, uncomment the following:
`Include conf/extra/httpd-ssl.conf`
4. The result should look as follows:  
![uncomments](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/uncommentssl.PNG)  
5. Now open the `httpd-ssl.conf` file and around line 123 modify the following lines to the following:  
> #   General setup for the virtual host  
> DocumentRoot "${SRVROOT}/htdocs/site2.tbd/"  
> ServerName site2.tbd  
6. Under **Server Certificate** uncomment `SSLCertificateFile` and modify as follows:
> SSLCertificateFile "${SRVROOT}/conf/Server.crt"  
7. Under **Server Private Key** uncomment `SSLCertificateKeyFile` and modify as follows:
> SSLCertificateKeyFile "${SRVROOT}/conf/Server.key"  
8. Now we need a self-signed certificate to remove the security error on the page.
9. Open a terminal and **cd** to `C:/Apache24/bin`. Type `.\openssl.exe`. Then type the following command to generate a self-signed certificate in your command prompt  
> `req -x509 -newkey rsa:2048 -keyout server.key -out server.crt -days 1000 -nodes`   
10. After you enter the command, you will be taken to a prompt where you can enter information about your website.
> ![sslform](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/sslinfo.PNG) 
12. Copy the two generated files (server.key and server.crt) from `C:\Apache24\bin` to `C:\Apache24\conf` folder. 
13. Your final result should look like this:  
> ![finalphoto](https://github.com/mayannamarie/WebServerProject1/blob/main/screenshots/finalphoto.PNG)

---
layout: post
title: Apache Setting (COMP7006_LAB_1)
description: >
    This is how to use Data Communication Library.
sitemap: false
group: true
hide_last_modified: true
image: /assets/img/nsad/wireshark_component/apache.png
---

## Apache server


## Fedora Install


### 1. Install httpd
```
    sudo dnf install httpd
```


### 2. Start Apache daemon
```
    systemctl start httpd
```
OR
```
    systemctl start httpd.service
```


### 3. Check if Apache running
```
    system status httpd
```
![HTTPD_STATUS](/assets/img/nsad/apache_setting/status.png "HTTPD_STATUS")

**The page served by httpd is a generic page included in the Linux distribution.**


#### PS) Make a server start during boot
```
    systemctl enable httpd.service
```



### 4. Change the 'http://localhost (HOST) homepage
```
    cd /var/www/html
```
> Create your own index.html
```
    nano -w index.html
```
> *You don't have to restart httpd<br/>*
> ***The page served by httpd is a generic page included in the Linux distribution.***


### 5. Check config file '**httpd.conf**' & '**userdir.conf**'
> 1\) Move to conf.d directory
>```
>    cd /etc/httpd/conf
>```
>
> 2\) Take a look at ***DocumentRoot*** section in httpd.conf file
>```
>    cat httpd.conf
>```
>
> 3\) Move to conf.d directory
> ```
>   cd /etc/httpd/conf.d
> ```
> 4\) Edit userdir.conf
> ```
>   nano -w userdir.con
> ```
> 5\) Comment out '**UserDir disable**' macro and and uncomment the '**UserDir public_html**'
> ```
>   <IfModule mod_userdir.c>
>       #
>       # UserDir is disabled by default since it can 
>       # confirm the presence of a username on the system (depending on home directory permissions).
>       # UserDir disabled
>       #
>       # To enable requests to /~user/ to serve the user's public_html directory, 
>       # remove the "UserDir disabled" line above, and uncomment the following line instead:
>       #
>       
>       UserDir public_html
> 
>   </IfModule>
> ```
> - This will allow people to open index.html of every single users you will gonna create<br/>
>
> 5\) RESTART httpd
> ```
>   systemctl restart httpd
> ```
> - Since you changed configuration file, you need to restart server

### 6. Create a NEW USER
> 1\) Check you are 'root' or 'host'
> ```
>   su
> ```
>
> 2\) Create a new user
>```
>   sudo useradd <user name>
>```
> In my case I call it 'bar'
>```
>   sudo useradd bar
>```
>
> 3\) Set password of the new user
>```
>   sudo passwd <user name>
>```
>
> 4\) Move to home directory and check if new user('bar') successfully created
> ```
>   cd /home
> ```
> ```
>   ls
> ```
>
> 5\) If created, **MOVE TO 'USER DIRECTORY'<br/>**
> - A new created user doesn't have permission to READ, WRITE, and EXECUTE the files of 'root' 
> - If you don't change to user directroy, you cannot do anything
> ```
>   cd <user name>
> ```


### 7. Login with new user acount
> 1\) Login
>```
>    su <user name>
>```
> 2\) You probably in a '**~**' directory that has no files (DON'T PANIC)
> ```
>    ls
> ```
> - NOTHING WILL SHOW IF YOU TYPE THIS
> - This is your 'home' directory 
>
> 3\) Create '**public_html**'
> ```
>   mkdir public_html
> ```
> ***This will now be the default document root directory***
>
> 4\) Move to '**public_html**' and create '**index.html**', which will user's web page
> ```
>   cd public_html
> ```
> ```
>   nano -w index.html
> ```
> 5\) Back to 'root' user after create index.html
> ```
>   exit
> ```
> 6\) Move to user directory
> ```
>   cd /home/<user name>
> ```
> 7\) Give user and people permission to '**public_html**'
> ```
>   chmod 711 .
> ```
> 8\) Test if it works
> ```
>   http://192.168.0.x/~<username>
> ```
> In my case, since I used 'bar'
> ```
>   http://192.168.0.x/~bar  OR  192.168.0.x/~bar
> ```

### 8. Adding password to access user's site
> 1\) As a root user, move to conf.d directory
> ```
>   cd /etc/httpd/conf.d
> ```
> 2\) Edit userdir.conf
> ```
>   nano -w userdir.con
> ```
> 4\) Comment out this part
> ```
>   # <Directory "/home/*/public_html">
>   #    AllowOverride FileInfo AuthConfig Limit Indexes 
>   #    Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec
>   #    Require method GET POST OPTIONS
>   # </Directory>
>```
>
> 5\) Add this part
> ```
>   <Directory /var/www/html/passwords> 
>       order deny, allow deny from all 
>   </Directory>
> ```
> 6\) Create a password on httpd tree
> ```
>   mkdir /var/www/html/passwords
> ```
> 7\) Move to 'html' directory 
> ```
>   cd /var/www/html
> ```
> 8\) Give permission to 'passwords' directory
> ```
>   chmod 755 passwords
> ```
> - ***Make sure the passwords directory is readable by user or group that your server runs under***
> 
> 9\) Move to passwords directory
> ```
>   cd passwords
> ```
> 10\) Create password
> ```
>   htpasswd -c < passwd file name > < user name > 
> ```
> 11\) Make sure '**< passwd file name >**' successfully created
> 
> 12\) Move to conf.d directory
> ```
>   cd /etc/httpd/conf.d
> ```
> 13\) Edit userdir.conf
> ```
>   <Directory /home/< user name >>  //<user name> will be 'bar'
>       AllowOverride None
>       AuthUserFile /var/www/html/passwords/< passwd file name > 
>       // < passwd file name> will be 'bar' 
>       # Group authentication is disabled
>       AuthGroupFile /dev/null
>       AuthName test
>       AuthType Basic 
>       <Limit GET>
>           require valid-user 
>           order deny, allow 
>           deny from all 
>           allow from all
>       </Limit>
>   </Directory>
> ```
> - The order, deny, and allow directives limit who will get a login panel.
> - If you want users to be able to use your server from outside your network, just omit these
directives
> - Otherwise, just replace domain with the domain name for your organization, or better
yet, specify your domain by using an IP address notation
> - If you replace domain with all, every user will get a password panel displayed on their
browser.
>
> 14\) RESTART httpd
> ```
>   systemctl restart httpd
> ```
> 15\) Go to your webpage
> ```
>   http://192.168.0.x/~bar
> ```
>![PASSWORD](/assets/img/nsad/apache_setting/password.png "PASSWORD")
> Once you get this result, you are good to go!

### 9. CHECK ERROS
> This command will show errors
> 1\) Move to '***httpd***' directory that is in '***log***' directory
```
    cd /var/log/httpd
```
> 2\) See the log 
```
    cat error_log
```

### 10. Final userdir.conf
```
 #
# UserDir: The name of the directory that is appended onto a user's home
# directory if a ~user request is received.
#
# The path to the end user account 'public_html' directory must be
# accessible to the webserver userid.  This usually means that ~userid
# must have permissions of 711, ~userid/public_html must have permissions
# of 755, and documents contained therein must be world-readable.
# Otherwise, the client will only receive a "403 Forbidden" message.
#
<IfModule mod_userdir.c>
	#
	# UserDir is disabled by default since it can confirm the presence
	# of a username on the system (depending on home directory
	# permissions).
	#
	# UserDir disabled

	#
	# To enable requests to /~user/ to serve the user's public_html
	# directory, remove the "UserDir disabled" line above, and uncomment
	# the following line instead:
	#
	UserDir public_html
</IfModule>


#Control access to UserDir directories.  The following is an example
#for a site where these directories are restricted to read-only.
#
#<Directory "/home/*/public_html">
#	AllowOverride FileInfo AuthConfig Limit Indexes
#	Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec
#	Require method GET POST OPTIONS
#</Directory>

<Directory /home/bar>
	AllowOverride None
	AuthUserFile /var/www/html/passwords/bar
	# Group authentication is disabled
	AuthGroupFile /dev/null
	AuthName test
	AuthType Basic
	<Limit GET>
    	require valid-user
    	order deny,allow
    	deny from all
    	allow from all
	</Limit>
</Directory>

<Directory /var/www/html/passwords>
	order deny,allow
	deny from all
</Directory>
```



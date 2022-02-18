---
title: "Apache web server: Basics"
---

# what is 

Ref: https://www.guru99.com/apache.html

**Q:** What is *virtual host*?

**Ans:** 

An Apache web server can host multiple websites on the *SAME* server. You do not need separate server machine and apache software for each website. This can achieved using the concept of Virtual Host or VHost. 

**key:** Host, Virtual host, VHost

**Q:** What is VHost?

**Ans:** VHost = Virtual Host

**Q:** How multiple sites are configured on a single web server host?

**Ans:**  Any domain that you want to host on your web server will have a separate entry in apache configuration file.

**Q:** What are the types of Apache Virtualhost?

**Ans:**  Two types are there:

1. Name-based Virtual host
2. Address-based or IP based virtual host

**Q:** What is a Name-based Virtual Host?

**Ans:** 

## From another site:

Ref: https://medium.com/swlh/apache-for-beginners-9d104225ec89

**Some Basic Commands**

Now, let’s go through some basic commands that you will need to manage your server!

You can enable your Apache site by using the command `a2ensite`(Apache 2 enable site) and disable it by using `a2dissite` (Apache 2 disable site).

**Q:** How to enable you Apache site?

**Ans:**

    sudo a2ensite YOUR_DOMAIN.conf
    sudo a2dissite YOUR_DOMAIN.conf

**Lingo:** 

> apache2 enable site = a2ensite  
  apache2 disable site = a2dissite 

**Q:** What is the domain name at the local apache web server?

**Ans:**

Suppose your config file name is `my_domain_1.conf`. Then your domain name is `my_domain_1`.


## new info

Ref: https://www.tecmint.com/list-enabled-virtual-hosts-in-apache-web-server/

**Q:** How to List All Virtual Hosts in Apache Web Server?

Apache virtual host configuration allows you to run multiple websites on the same server, that means you can run more than one website on the same Apache web server. You simply create a new virtual host configuration for each of your websites and restart the Apache configuration to start serving the website. 

On Debian/Ubuntu, the recent version of Apache configuration files for all virtual hosts are stored in the `/etc/apache2/sites-available/` directory. So, it makes really difficult to go through all of these virtual host configuration files to fix any configuration errors.

To make things easier, in this article we will show you how to list all enabled apache virtual hosts on a web server using a single command on the terminal. This method will also help you to see a few other useful apache configurations.

This is practically helpful in a scenario where you are assisting a company to fix their web server issues remotely, yet you do not know their current apache web server configurations, in regards to virtual hosts.

It will help ease searching for the virtual host of a specific website in the apache config files and assist in troubleshooting any Apache issues, where you’ll, in most cases start with checking of the currently enabled virtual hosts before looking into the logs. 

To list all enabled virtual hosts on the web server, run the following command in a terminal.


    # apache2ctl -S   [On Debian/Ubuntu]
    # httpd -S # Note: maybe you need to install it

    AH00558: apache2: Could not reliably determine the server's
	fully qualified domain name, using 127.0.1.1. Set the  
	'ServerName' directive globally to suppress this message
    VirtualHost configuration:
    *:80                   is a NameVirtualHost
         default server 127.0.1.1 (/etc/apache2/sites-enabled/000-default.conf:1)
         port 80 namevhost 127.0.1.1 (/etc/apache2/sites-enabled/000-default.conf:1)
         port 80 namevhost www.site1.local (/etc/apache2/sites-enabled/site1.local.conf:1)
                 alias site1.local
    ServerRoot: "/etc/apache2"
    Main DocumentRoot: "/var/www/html"
    Main ErrorLog: "/var/log/apache2/error.log"
    Mutex mpm-accept: using_defaults
    Mutex watchdog-callback: using_defaults
    Mutex rewrite-map: using_defaults
    Mutex default: dir="/var/run/apache2/" mechanism=default 
    PidFile: "/var/run/apache2/apache2.pid"
    Define: DUMP_VHOSTS
    Define: DUMP_RUN_CFG
    User: name="www-data" id=33 not_used
    Group: name="www-data" id=33 not_used


Now the above site is diabled:

    sudo a2dissite site1.local.conf

then:

    sudo systemctl reload apache2
	
then:

    apache2ctl -S

You get:


    AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 127.0.1.1. Set the 'ServerName' directive globally to suppress this message
    VirtualHost configuration:
		*:80                   127.0.1.1 (/etc/apache2/sites-enabled/000-default.conf:1)
	ServerRoot: "/etc/apache2"
	Main DocumentRoot: "/var/www/html"
	Main ErrorLog: "/var/log/apache2/error.log"
	Mutex default: dir="/var/run/apache2/" mechanism=default 
	Mutex mpm-accept: using_defaults
	Mutex watchdog-callback: using_defaults
	Mutex rewrite-map: using_defaults
	PidFile: "/var/run/apache2/apache2.pid"
	Define: DUMP_VHOSTS
	Define: DUMP_RUN_CFG
	User: name="www-data" id=33 not_used
	Group: name="www-data" id=33 not_used

## Setting Up Virtual Hosts

Ref: https://medium.com/swlh/apache-for-beginners-9d104225ec89

What if you want to host multiple websites on the same server? Virtual hosts let you do that. They are a method for multiple domain names to use the same physical server and share computational resources.

First, if you want to host multiple sites on the same server, you probably won’t want to store all your web content in `/var/www/html`. You could create a separate directory for each one of your domains. Let’s say that we are creating a site with the domain name “mysite.com”.

    sudo mkdir /var/www/mysite.com
	
You can then fill web content for that domain in the domain-specific directory. This command creates an empty index file for your site.	

    sudo touch /var/www/mysite.com/index.html
	
The contents of that index file could be as simple as:

	<html>
		<body>
			<h1>This is your index page :) </h1>
		</body>
	</html>

For Apache to serve your content, it will need configuration files for this specific domain. So you need to create a configuration file named “YOUR_DOMAIN.conf” in the “sites-available” directory.	


    sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/mylocalsite1.com.conf
	
	sudo nano /etc/apache2/sites-available/mylocalsite1.com.conf
	
The file:


	<VirtualHost *:80>
        ServerAdmin admin@mylocalsite1.com
        ServerName mylocalsite1.com
        DocumentRoot /home/pankaj/project/web/apache/mylocalsite1.com
        ErrorLog /home/pankaj/project/web/apache/mylocalsite1.com/error.log
        CustomLog /home/pankaj/project/web/apache/mylocalsite1.com/access.log combined
	</VirtualHost>



Now enable the site:

	sudo a2ensite mylocalsite2.com.conf 

Cheick

	sudo apache2ctl configtest
	sudo systemctl reload apache2

To see:

	ls /etc/apache2/sites-enabled/
	mylocalsite1.com.conf  mylocalsite2.com.conf
	ls /etc/apache2/sites-available/
	000-default.conf  default-ssl.conf  mylocalsite1.com.conf  mylocalsite2.com.conf  site1.local.conf

file:

    sudo nano /etc/apache2/apache2.conf


The Apache web server will not be able to access the folder in the HOME folder. So change this to `Allow from all`.

    <Directory /home/pankaj/project/web/apache/mylocalsite1.com/>
         Options Indexes FollowSymLinks
         AllowOverride None
         Require all granted
         Allow from all
    </Directory>

Disable the site:

    sudo a2dissite mylocalsite1.com.conf
	
the above thing gives the site at `localhost`. but you cannot access more than one site on the same server. So what to do for it?

    sudo nano /etc/hosts


Open the above file.


    127.0.1.1    pankaj−desktop
    127.0.1.1    site1.com
    127.0.1.1    site2.com
    127.0.1.1    site3.com

site

    $ sudo a2enmod rewrite
    Module rewrite already enabled

the response was the second line above.

for laravel change the document root to `public` only

then you need to change the permission of access to folders also.


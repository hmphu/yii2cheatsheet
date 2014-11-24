# Install Yii Framework 2 #
You can install Yii in two ways, using Composer or by downloading an archive file. The former is the preferred way, as it allows you to install new extensions or update Yii by simply running a single command.
## Installing via Composer ##
    composer global require "fxp/composer-asset-plugin:1.0.0-beta3"
    composer create-project --prefer-dist yiisoft/yii2-app-basic basic
Tip: If you want to install the latest development version of Yii, you may use the following command instead, which adds a stability option:
    composer create-project --prefer-dist --stability=dev yiisoft/yii2-app-basic basic
## Installing from an Archive File ##
Installing Yii from an archive file involves three steps:

Download the archive file from yiiframework.com.
Unpack the downloaded file to a Web-accessible folder.
Modify the config/web.php file by entering a secret key for the cookieValidationKey configuration item (this is done automatically if you are installing Yii using Composer):

    // !!! insert a secret key in the following (if it is empty) - this is required by cookie validation
    'cookieValidationKey' => 'enter your secret key here',
## Recommended Apache Configuration ##
    # Set document root to be "basic/web"
    DocumentRoot "path/to/basic/web"
    
    <Directory "path/to/basic/web">
    # use mod_rewrite for pretty URL support
    RewriteEngine on
    # If a directory or a file exists, use the request directly
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    # Otherwise forward the request to index.php
    RewriteRule . index.php
    
    # ...other settings...
    </Directory>
## Recommended Nginx Configuration ##
    server {
	    charset utf-8;
	    client_max_body_size 128M;
	    
	    listen 80; ## listen for ipv4
	    #listen [::]:80 default_server ipv6only=on; ## listen for ipv6
	    
	    server_name mysite.local;
	    root/path/to/basic/web;
	    index   index.php;
	    
	    access_log  /path/to/basic/log/access.log main;
	    error_log   /path/to/basic/log/error.log;
	    
	    location / {
		    # Redirect everything that isn't a real file to index.php
		    try_files $uri $uri/ /index.php?$args;
	    }
	    
	    # uncomment to avoid processing of calls to non-existing static files by Yii
	    #location ~ \.(js|css|png|jpg|gif|swf|ico|pdf|mov|fla|zip|rar)$ {
	    #try_files $uri =404;
	    #}
	    #error_page 404 /404.html;
	    
	    location ~ \.php$ {
		    include fastcgi.conf;
		    fastcgi_pass   127.0.0.1:9000;
		    #fastcgi_pass unix:/var/run/php5-fpm.sock;
		    try_files $uri =404;
	    }
	    
	    location ~ /\.(ht|svn|git) {
	    	deny all;
	    }
    }
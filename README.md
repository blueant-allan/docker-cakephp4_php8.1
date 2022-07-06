## Dockerfile development configuration

For CakePHP version 4.x running on PHP version 8.1. With Ubuntu 22.04 as base image


Stack

* Ubuntu 22.04
* Nginx
* PHP-FPM 
* PHP version 8.1.2
* CakePHP vesion 4.x
* Mail Hog

Loaded PHP Extensions

* Mysql
* Intl
* Mbstring
* Zip
* Xml
* Sqlite3


## Compile the docker file

```
docker build -t cakephp4_php8.1-image -f Dockerfile.dev .
```

## Create instance of the container

```
docker run -p 8080:80 -dit --name conainer_name-web --env MAILHOG_SMTP_IP_ADDR=172.17.0.3 --mount type=bind,source="$(pwd)",target=/var/www/html cakephp4_php8.1-image
```


## Manage the container

```
docker exec -it conainer_name-web bash
```


## Usage

1. You can start by create a CakePHP project via composer

```
composer create-project --prefer-dist cakephp/app:~4.0 <project_name>
```

2. MailHog container dependency. It is assumed that you have a MailHog container 
running in your environment. If you do not have one execute the following on 
your command line to create one. You can then access your MailHog UI by going 
to this address http://localhost:8025

```
# Create a MailHog container
docker run -dit --name mailhog -p 1025:1025 -p 8025:8025 mailhog/mailhog
```


3. Build the dockerfile configuration and create a container for it.


4. Now that you have your container setup, let us setup CakePHP

```
docker exec -it <project-name> bash
	
# let us complete the CakePHP installation
php composer.phar install
```

This document assumes that you have composer.phar file.


5. You should be able to load your web-application from your browser with the port you incidated above. Example: http://localhost:8080


6. Update your app-config file so that you can connect to your database


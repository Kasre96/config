# Deploying Laravel application on a Live Server

This config is mostly for CentOS 7, but flow is same for almost all Linux distributions

[Inspiration - TecAdmin.net](https://tecadmin.net/install-laravel-framework-on-centos/)

1. Configure `ssh` access for yourself in the server. You may require sudo privileges

2. Install **LAMP** or **LEMP** stack. This is a stack containing Linux(presumed to be alredy installed), a web server, MySQL database and PHP. LAMP containes **Apache** web server while LEMP contains **NGINX**

    Apache is more preferred due to ease of configuration. ([Link](https://tecadmin.net/install-apache-php-fpm-centos-8/) for Apache and [Link](https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-ubuntu-18-04) for Nginx)

    While installing php, make sure that all dependencies and extensions required by laravel are installed [Requirements](https://laravel.com/docs/5.7/installation#server-requirements)

    Also install composer ([Link](https://linuxize.com/post/how-to-install-and-use-composer-on-centos-7/))

3. By now you should have Apache, PHP, MySQL and composer installed.
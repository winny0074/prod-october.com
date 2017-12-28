1. Installation
    There are three ways to install october. We  used composer instalation method
    run:
    
    #install october with composer command
    $ composer create-project october/october october

    frontend : http://localhost/cms/laravel/october/
    backend: http://localhost/cms/laravel/october/backend

    # init database
      -first create your database
      - run :
        $ php artisan october:up     (this will create all needed table in your database with some records)

2. virtual host
    We create two domains dev-october.com and prod-october.com
    These both will listen on port 80 and will use the same ip address 127.0.0.1.

    # How to set up virtual host
    ref1: https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-debian-8
    ref2: https://doc.ubuntu-fr.org/tutoriel/virtualhosts_avec_apache2

    Step 1 — Creating the Directory Structure

    $ sudo mkdir -p /var/www/html/cms/laravel/dev-october.com/public_html/
    $ sudo mkdir -p /var/www/html/cms/laravel/prod-october.com/public_html/

    copy october to /var/www/html/cms/laravel/dev-october.com/public_html/
    $ cp -R october_path /var/www/html/cms/laravel/dev-october.com/public_html/
    $ cp -R october_path /var/www/html/cms/laravel/prod-october.com/public_html/

    change access right and ownership for both domain
    $chown -R www-data:www-data /var/www/html/cms/laravel/dev-october.com/
    $chmode -R ugo+wrx /var/www/html/cms/laravel/dev-october.com/

    Step 3 — Create New Virtual Host Files

    $ sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/dev-october.com.conf
    modify file with:

            ServerAdmin webmaster@dev-october
            ServerName  dev-october.com
            ServerAlias www.dev-october.com
            DocumentRoot /var/www/html/cms/laravel/dev-october.com/public_html/

    Do the same with prod-october.com

    Step 4 — Enabling the New Virtual Host Files

    $ sudo a2ensite dev-october.com.conf
    $ sudo a2ensite prod-october.com.conf

    #reload appach config
    $ service apache2 reload

    $ service apache2 stop
    $ service apach2 start

    Step 5 — Setting Up Local Hosts File

    $ sudo vim /etc/hosts

    add :
    127.0.0.1 dev-october.com
    127.0.0.1 prod-october.com

    Step 6 — Testing Your Results

    if you load from your browser, 

    frontend: dev-october.com and prod-october.com 
    backent: dev-october.com/backend | prod-october.com/backend

    !! if backend doesnot work, verify if in your root path, you have .htaccess

3. Database configuration

set your database configuration in config/database.php

e.g

 'mysql' => [
            'driver'    => 'mysql',
            'host' => env('DB_HOST', 'localhost'),
            'port' => env('DB_PORT', '3306'),
            'database' => env('DB_DATABASE', 'october'),
            'username' => env('DB_USERNAME', 'root'),
            'password' => env('DB_PASSWORD', 'root'),
            'charset'   => 'utf8',
            'collation' => 'utf8_unicode_ci',
            'prefix'    => '',
        ],

3. environment



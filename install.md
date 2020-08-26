### Bacic 

* __Step 1:-__ Download the codeigniter https://codeigniter.com/download
* __Step 2:-__ download project move to tha xampp->httdocs->and your folder
* __database_connect:-__ Go to the application/config/database.php
* __config file change:-__ Go to the application/config/config.php  (Full path of the project folder)
```php 
$config['base_url'] = 'http://your-domain.com';
$config['index_page'] = '';
```
* __.htaccess:-__ .htaccess file move the route file and paste code
```php
<IfModule authz_core_module>
  RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php/$1 [L]
</IfModule>
```

* __Routes Define:-__  application/congif/routes.php

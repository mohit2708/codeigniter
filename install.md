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
### How to use a sub folder in default controller route in CodeIgniter.
create file application > core > MY_Router.php
```php
<?php

class MY_Router extends CI_Router {
    protected function _set_default_controller() {

        if (empty($this->default_controller)) {

            show_error('Unable to determine what should be displayed. A default route has not been specified in the routing file.');
        }
        // Is the method being specified?
        if (sscanf($this->default_controller, '%[^/]/%s', $class, $method) !== 2) {
            $method = 'index';
        }

        // This is what I added, checks if the class is a directory
        if( is_dir(APPPATH.'controllers/'.$class) ) {

            // Set the class as the directory

            $this->set_directory($class);

            // $method is the class

            $class = $method;

            // Re check for slash if method has been set

            if (sscanf($method, '%[^/]/%s', $class, $method) !== 2) {
                $method = 'index';
            }
        }

        if ( ! file_exists(APPPATH.'controllers/'.$this->directory.ucfirst($class).'.php')) {

            // This will trigger 404 later

            return;
        }
        $this->set_class($class);
        $this->set_method($method);
        // Assign routed segments, index starting from 1
        $this->uri->rsegments = array(
            1 => $class,
            2 => $method
        );
        log_message('debug', 'No URI present. Default controller set.');
    }
}
```
```php
$route['default_controller'] = 'subfolder/controller/function';
```
* __Routes Define:-__  application/congif/routes.php

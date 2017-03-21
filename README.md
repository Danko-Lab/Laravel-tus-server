Laravel 4.2 Tus Server
======

Library in laravel PHP 4.2 for [tus server](http://www.tus.io/) (tus protocol 1.0)

Installation
------------

use [composer](http://getcomposer.org/)

Server Usage
------------

```php

/**
 * Set route function for the upload URL in 'routes.php'
 */
Route::any("upload", function(){
    return TusUpload("");
});

Route::any("upload/{file}", function($file){
    return TusUpload($file);
});


/**
 * Implement the TusUpload function using the Tus protocol.
 */
public static function TusUpload( $file ){
   $request = \Illuminate\Http\Request::createFromGlobals();
   $tmp_dir = ini_get('upload_tmp_dir') ? ini_get('upload_tmp_dir') : sys_get_temp_dir();
	
   // Create and configure server
   $server = new TusServer($tmp_dir, $request, $debug = true );
   // Run server
   $server->process(true);
}
   
```

If you are with an Apache server, add an .htaccess file to redirect all request in the php page (without that, your PATCH call failed), like :

```bash
RewriteEngine on

RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^(.*)$ index.php [QSA,L]
```


Author
------

Zhong Wang <wzhy2000@hotmail.com>.

This library is based on ZfTusServer library (https://github.com/Orajo/zf2-tus-server) by Jaroslaw Wasilewski <orajo@windowslive.com> .

License
-------

[MIT](http://opensource.org/licenses/MIT)

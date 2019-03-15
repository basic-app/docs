2. Add library in the application class loader config file: "/Config/Autoload.php".

```
$psr4 = [
    ...
    'BasicApp\Bootstrap4' => dirname(dirname(COMPOSER_PATH)) . '/vendor/basic-app/bootstrap4'
];
```

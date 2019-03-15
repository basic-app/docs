2. Add library in the application class loader config file: "/Config/Autoload.php".

```
$psr4 = [
    ...
    'BasicApp\Bootstrap4' => dirname(dirname(COMPOSER_PATH)) . '/vendor/basic-app/bootstrap4'
];
```

The basic part of the system is a micro-core, which does not depend on external libraries. Classes from the Basic App Core package can be used in any CodeIgniter 4 application.
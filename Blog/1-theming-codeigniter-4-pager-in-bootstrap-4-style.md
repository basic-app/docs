CodeIgniter 4 pager generates a non-compatible with Bootstrap 4 HTML code. We offer you to use a ready-made solution to design a CodeIgniter 4 pager in Bootstrap 4 style.

### Installation:

1. Install the "basic-app/bootstrap4" library via Composer.

```
composer require "basic-app/bootstrap4:dev-master"
```

2. Add library in the application class loader config file: "/Config/Autoload.php".

```
$psr4 = [
    ...
    'BasicApp\Bootstrap4' => dirname(dirname(COMPOSER_PATH)) . '/vendor/basic-app/bootstrap4'
];
```

3. Add the Bootstrap 4 template in the application pager config file: "/Config/Pager.php".

```
public $templates = [
    ...
    'bootstrap4' => 'BasicApp\Bootstrap4\Views\pager'
];
```

### Additional Settings:

You can specify how many links you need to create on each side of the active link. Add a public variable $surroundCount in the pager config file: "/Config/Pager.php".

```
public $surroundCount = 3;
```

### Using:

```
echo $pager->links('default', 'bootstrap4');
```
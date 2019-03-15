CodeIgniter 4 pager generates a non-compatible with Bootstrap 4 HTML code. We offer you to use a ready-made solution to design a CodeIgniter 4 pager in Bootstrap 4 style.

### Installation:

1. Install the "basic-app/bootstrap4" library via Composer:

```
composer require "basic-app/bootstrap4:dev-master"
```

2. Add the Bootstrap 4 template in the pager config file: "/Config/Pager.php":

```
public $templates = [
    ...
    'bootstrap4' => 'BasicApp\Bootstrap4\Views\pager'
];
```

### Using:

```
echo $pager->links('default', 'bootstrap4');
```

### Additional Settings:

You can specify how many links you need to create on each side of the active link. Add a public variable "$surroundCount" in the pager config file: "/Config/Pager.php".

```
public $surroundCount = 3;
```

You can set the "$surroundCount" variable from application code dynamically:

```
$config = config('Pager'); // get pager config

$surroundCount = $config->surroundCount; // save current value

$config->surroundCount = 5; // set new value

echo $pager->links('default', 'bootstrap4'); // generate pagination

$config->surroundCount = $surroundCount; // restore original value 

```
Create layouts in CodeIgniter 4
===============================

Ready-made solution to create layouts in CodeIgniter 4.

CodeIgniter 4 does not have have an engine for displaying layouts. You can implement the most appropriate layouts for each application, but it is convenient to have a unified methods. We offer you to use a ready-made solution to display layouts in CodeIgniter 4.

Installation via Composer:

`composer require "basic-app/core:dev-master"`

## Usage

```
class Welcome extends \BasicApp\Controller
{
    protected $layout = 'main';
    
    function index()
    {
        return $this->render('index', ['param1' => 'value']);
    }
}
```

The Basic App Core module has no dependencies, it can be used in any CodeIgniter 4 based project.
# [Basic App Layouts](http://basic-app.com/docs/views/layouts.md)

[Documentation](/docs) / [Views](/docs/views)

#### Usage:

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
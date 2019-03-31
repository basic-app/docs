# [Basic App Layouts](http://basic-app.com/docs/core/views/layouts.md)

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
How to do basic CRUD in CodeIgniter 4
=====================================

Ready-made solution to do basic CRUD in CodeIgniter 4.

One of the most tedious tasks in the development of the site is to write a lot of controllers that perform the same function. Especially many controllers of the same type are located in the backend area. One of the solutions to the problem is to inherit CRUD controllers from some basic class that implements the base CRUD. We made a base class for CRUD controller for CodeIgniter 4. 

Install "Basic App Core" library:

`composer require "basic-app/core:dev-master"`

To perform basic operations with a model, quite a bit of additional data is needed, since all master data is already in the model, but it is declared as protected. To make the CRUD controller work, you need to implement the getReturnType() and getPrimaryKey() methods in the model. In order not to do this in each model, you can inherit your models from "BasicApp\Model" and "BasicApp\Entity" classes.

Inherit the controller from "BasicApp\AdminCrudController" class.

```
class Menu extends \BasicApp\AdminCrudController
{

    protected $modelClass = \BasicApp\Site\Models\Menu::class;

    protected $viewPath = 'BasicApp\Site\Views\Admin\Menu';

    protected $returnUrl = 'admin/menu';

    protected $perPage = 10;
    
    protected $orderBy = 'menu_id ASC';

}
```

That`s it! You can make views on your own, they are passed parameters: $elements, $pager, $model, $errors, on the basis of which you make the necessary page layout.

In one article it is difficult to give an exhaustive instruction with all the nuances of use, the fastest way to learn is to simply look at the working example of use. You can do it in our module "Basic App Site", which contains functionality for managing text pages, blocks, and menus.

[https://github.com/basic-app/module-site](https://github.com/basic-app/module-site)

The code is distributed under the MIT license, you can freely use it in your projects.
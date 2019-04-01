# [Working with menus](http://basic-app.com/docs/core/views/menus.md)

[Documentation](/docs) / [Core](/docs/core) / [Views](/docs/core/views)

In the Basic App backend, you can manage your site menu. You can add new menus, add and remove menu items, turn menu items on and off. For each menu item, you can configure additional attributes that allow you to customize them on the site.

The simpliest way to connect a menu to a template is to get its items as objects, and on the basis of them, generate the menu as HTML.

#### A simple example of menu generation:

```
use BasicApp\Site\Models\MenuModel;

foreach(MenuModel::getMenuItems('my_menu', true, ['menu_name' => 'Social Buttons']) as $item)
{
    echo '<a href="' . $item->item_url . '">' . $item->item_name . '</a>';
}
```

The `MenuModel::getMenuItems()` method takes as its first parameter the menu identifier. If the second parameter is true, the menu will be automatically created if it does not exist. By the third parameter, you can pass menu attributes with which it will be created if it does not exist. This parameter does not change the properties of an existing menu, these are only default values when it is created.

#### Menu attributes:

  - Menu ID (menu_id)
  - Menu Name (menu_name)
  - Menu UID (menu_uid)
  - Default Item HTML Class (menu_default_item_class)
  - Default Item Link HTML Class (menu_default_item_link_class)
  - Default Item Icon (menu_default_item_icon)
  
The `MenuModel::getMenuItems()` method returns objects of the type `BasicApp\System\Models\MenuItem`, for which the `item_enabled` (Item Enabled) property is set to active. The results are sorted by the value of the field `item_sort` (Item Sort). You decide how to use additional fields if you generate your menu manually. 
  
#### Attributes of a menu item object:

  - Item ID (item_id)
  - Menu ID (item_menu_id)
  - Item UID (item_uid)
  - Item Name (item_name)
  - Item Enabled (item_enabled)
  - Item HTML Class (item_class)
  - Item Link HTML Class (item_link_class)
  - Item Icon (item_icon)
  - Item Sort (item_sort)
  
#### Generating the menu via widgets
  
A more correct way to generate menus is through menu widgets. In this case, you transfer menu items to the menu generation widget as a typed array:

#### Array menu items:

```
$menuItems = [
    [
        'label' => 'Item Name',
        'url' => '/page/url',
        'icon' => 'fa fa-icon',
        'options' => [
            'id' => 'menu-my_menu-item-3',
            'class' => 'li-class'
        ],
        'linkOptions' => [
            ‘class’ => ‘a-class'
        ]
    ]
];
```

Such an array can be obtained using the `menu_items` function, which is in the `menu` helper.

```
function menu_items(string $menu, bool $create = false, array $params = []) : array
```

Parameters passed to the function `menu_items()`, similar to the parameters `MenuModel::getMenuItems()`, which have already been described above.

Menu generation widgets are not included in the Basic App, but are inside themes. We recommend that developers try to adhere to the same name of the parameters, but the final choice rests with the theme developer. See the documentation for the specific topic you are using for information on how to generate a menu as HTML code from a given parameter array.
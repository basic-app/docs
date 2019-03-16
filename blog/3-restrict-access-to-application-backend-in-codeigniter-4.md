Restrict access to application backend in CodeIgniter 4
=======================================================

Instruction how to to restrict access to application backend in CodeIgniter 4.

The easiest way to restrict access to application backend, is to check the address of the current page, and if it starts with /admin, then check a logged user rights. This can be implemented through filters, that appeared in the fourth version of the framework.

Add a "Basic App Core" library contains an admin filter via Composer:

`composer require "basic-app/core:dev-master"`

Set up a new filter in application filters config file: "/Config/Filters.php":

```
public $aliases = [
    ...
    'admin' => \BasicApp\AdminFilter::class
];

...

public $filters = [
    ...
    'admin' => [
        'before' => ['admin', 'admin/*']
    ]
];
```

### Extending

If you have an another implementation of users and rights, then you can inherit your version of "BasicApp\AdminFilter" class from "BasicApp\BaseAdminFilter" class and override "currentUserId", "checkAccess" and "getUser" methods.

[Extending Core Classes](/blog/2-extending-core-classes.md)
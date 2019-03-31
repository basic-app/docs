composer create-project --stability=dev --remove-vcs --prefer-dist basic-app/basic-app demoapp

2. Add library in the application class loader config file: "/Config/Autoload.php".

```
$psr4 = [
    ...
    'BasicApp\Bootstrap4' => dirname(dirname(COMPOSER_PATH)) . '/vendor/basic-app/bootstrap4'
];
```

The basic part of the system is a micro-core, which does not depend on external libraries. Classes from the Basic App Core package can be used in any CodeIgniter 4 application.

The basic application contains the base modules already connected via Composer.

## Table of Content

  - [Installation](installation.md)
  - Creating Modules
  - Extending Core Classes
  - Extending Views
  - Using Events  
  - Backend
  - Using RBAC
  - Actions
  - Behaviors
  - CRUD
  - [Themes](blog/themes.md)
  - Models
  - Entities
  - Relations
  - Internationalization
  - Translate Model Attributes
  - Filter Model
  - Store Configs in Database
  - Image Manipulation
  - Cron Tasks
  - Sending E-mail
  - [Pagination](blog/1-theming-codeigniter-4-pager-in-bootstrap-4-style.md)
  
  We provide technical support to system users and developers on our support forum. 

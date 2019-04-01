# [Extending base classes of the Basic App](http://basic-app.com/docs/extending-base-classes.md)

[Documentation](/docs)

The classes of core and modules of the Basic App have the necessary functionality to create a typical site, but to create a real project, you will most likely need to complete them with new functions. To do this, you will need to override the necessary classes in your application.

All Basic App classes consist of two files. The first file contains the working code of the class, these classes are abstract, and contain the suffix Base in its name. The second file is called the name of the class that is used in the code, and the class in this file extends the abstract base class. To complete the base class with new functions, you need to create the required class in the working folder of the application and inherit it from the base abstract class.

#### Example of use:

Let's say you want to complete the class of post in blog with new functions. The main entity class for a blog is the `BasicApp\Blog\Models\Blog` class, which extends the `BasicApp\Blog\Models\BlogBase` class. You need to create a new class inside the working directory of the application, for example in the `/app/ThirdParty/BasicApp/Blog/Models/BlogPost.php` file.

Technically, you can create a new class anywhere, but we recommend using this location for new classes to ensure consistency of projects on the Basic App. You can simply copy the file of the original class, which is located in the `/vendor/basic-app/module-blog/Models/BlogPost.php` file to a new location.

Add the desired functionality in the new file. After that, you need to connect a new class before the system will look for it through the class autoloader. The simplest and most effective solution is to make a simple call to the `require_once` operator for a new file. We offer to use CodeIgniter4 `pre_system` hook.

Open the `/app/Config/Events.php` file and add the `require_once` to the `pre_system` event handler:

```
Events::on('pre_system', function() {
    require_once APPPATH . '/ThirdParty/BasicApp/Blog/Models/BlogPost.php';
});
```

Pay attention that most likely in your application there is already a handler for the `pre_system` event, and you only need to add a `require_once` call to it for the new file.

Overriding base classes in your application is a normal practice with Basic App. The ideology of the system is based on the fact that the common code between the sites is in the modules, and the project-specific code is inside the working directory of the application.
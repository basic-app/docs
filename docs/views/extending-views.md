# [Overriding of the design templates in the Basic App](http://basis-app.com/docs/views/extending-views.md)

[Documentation](/docs) / [Views](/docs/views)

The Basic App offers to use ready-made modules to create basic sections of the site. These modules contain basic display templates for generating the visual part of their pages. To change completely the standard layout of the modules you need to make sure that they generate completely different HTML code, such as required for integration into the application of the new design. To solve this problem, you can override any View file from any Basic App module in your application on the Basic App.

CodeIgniter 4 for rendering templates offers to use view function.

```
function view(string $name, array $data = [], array $options = [])
```

The `view()` function looks for the `$name` display file and gets its contents. The file may be inside a namespace, but it is necessarily one specific file. To change the code that the view function returns, you need to edit the contents of the target view file, but this is not possible if the file is in a module inside the Composer package.

To solve this problem, the Basic App modules render their mappings through the special function `app_view()`, whose parameters are exactly the same as in the `view()` framework function. 

```
function view(string $name, array $data = [], array $options = [])
```

The `app_view()` function, before outputting the `$name` file, checks whether it was redefined in the main application inside the `/app/Views` folder, and if it finds it, it outputs this file, and if it does not, it displays the original file.

#### Example of use:

Let`s say you want to change the design of  a blog post page. This template is in the file:

```
/vendor/basic-app/module-blog/Views/BlogPost/view.php
```

CodeIgniter 4 finds this file under the alias `BasicApp\Blog\BlogPost`, and to override it in your application, you need to create a similar file inside the `/app/Views directory`. In this case the full name of the file will be like this:

```
/app/Views/BasicApp/Blog/BlogPost/view.php
```

In the new file you can generate the HTML code you need, using the same parameters that are used in the original file. The `app_view()` function works through the original `view()` function of the framework, so its use does not contradict the best practices of working with the framework.

Please note that most of the design templates from the Basic App modules, for rendering HTML code, use widgets inside the module of theme. To simply change the design of the site, a better solution would be to create a new module of theme. 

[Read more about themes](/docs/views/themes.md)

By connecting a different theme to your site, you will change the appearance of all the Basic App modules at once, without having to redefine each display template individually. You can combine both methods to solve your tasks.

"Basic App Dev Team" provides services for the creation of the modules of themes from HTML templates.
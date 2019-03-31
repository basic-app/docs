# [Translation of the names of attributes of CodeIgniter 4 models in the Basic App](http://basic-app.com/docs/core/models/translate-attribute-labels.md)

[Documentation](/docs) / [Core](/docs/core) / [Models](/docs/core/models)

You define what you consider to be the names of the attributes in the `$labels` property in your model, which is inherited from the `BasicApp\Core\Model` class. In the Basic App there is no rule that the attribute is a required field in the database. This can be any message associated with a model.

[Read more about model attributes in CodeIgniter 4]

To make the function of translating the names of the attributes of the model into the backend, define the `$translations` variable in your model. The value of the variable is the name of the category in which the translations will appear in the backend of your website on CodeIgniter 4. 

### Example of translation of CodeIgniter 4 model attributes:

```
class MyModel extends \BasicApp\Core\Model
{
    protected $translations = 'my-model';

	protected $labels = [
		'field_1' => 'Field 1 Name',
		'field_2' => 'Field 2 Name',
		'any_name' => 'Name',
		'hello_message' => 'Hello message text here.'
	];
}
```

In addition to the attributes defined in $labels, you can dynamically get translations for any strings associated with your Basic App model through the `t()` function, which is defined in the `BasicApp\Core\Model` class.

### Function for localization of CodeIgniter 4 model resources:

```
public function t(string $str, array $params = []) string
```

### Example of getting the translation:

```
echo MyModel::t('Any String Text {param}.', ['{param}' => 'Value']); 
```

As a result of this example, the text will be "Any String Text Value", translated in the backend to the current application language. The text for translation will appear in the category "my-model", because it was defined in the `$translations` property in the model class.

Pay attention, the Basic App does not perform automated translation. Texts that you localize through the `t()` function and `MyModel::t()` fall into the backend section with translations, where the site administrator can translate them independently.

[Read more about translations in the Basic App]
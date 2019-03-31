Labels of CodeIgniter 4 model attributes in Basic App
=====================================================

[Documentation](/docs) / [Core](/docs/core) / [Models](/docs/core)

If you want to automate the receipt of the names of the attributes of CodeIgniter 4 models, then you can use the ready-made functions from the Basic App. In any model that inherits from BasicApp\Core\Model, you can define the protected attribute $labels. The value of this attribute is an array, which lists the names of the attributes of the model, and any other elements associated with this model. 

```
class MyModel extends \BasicApp\Core\Model
{
	protected $labels = [
		'field_1' => 'Field 1 Name',
		'field_2' => 'Field 2 Name',
		'any_name' => 'Name',
		'hello_message' => 'Hello message text here.'
	];
}
```
Anywhere in the application, you can get the value of this attribute with the static `label()` function by passing the identifier of the attribute for which you want to get a name to it with a parameter.

### Function of getting the name of a specific attribute

```
public static function label(string $field, $default = null) : string;
```

You can get the attributes as a list with the `getLabels()` function which returns an array of attribute names.

### Function of getting a list of attribute names

```
public static function getLabels() : array;
```

Always get the names of the attributes of the model through these functions, and not directly from the variable. Firstly, it will allow you to override the getting of attributes in the descendant classes, and secondly, in the Basic App there are functions for translating model attributes that work through these functions.

[Translation of model attributes](/docs/core/models/translate-attribute-labels)

## Entity class

CodeIgniter 4 models are divided into Model and Entity, and Entity can be a simple array. To maintain array support, all basic functions for working with attribute names are implemented in the model class. For ease of use, in the `BasicApp\Entity` class there are getters, using which you can get the names of the model attributes from the entity.

```
function getLabels() : array;

function label(string $field, $default = null) : string
```

These functions do not have their own implementation in the entity class, 
they call similar functions from the model. If you want to override or supplement the list 
of names of attributes, then this should be done in the model class. Pay attention that in the model these functions are static, and in the entity are not static.

### Example of getting the name of the model attribute:

```
$labelName = MyModel::label('field_1');
```
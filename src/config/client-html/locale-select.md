
# currency
## decorators/global

```
client/html/locale/select/currency/decorators/global = Array
(
)
```

* Default: Array
(
)



## decorators/local

```
client/html/locale/select/currency/decorators/local = Array
(
)
```

* Default: Array
(
)



## name

Name of the currency part used by the locale selector client implementation

```
client/html/locale/select/currency/name = Standard
```

* Default: Standard
* Type: string - Last part of the client class name
* Since: 2014.09

Use "Myname" if your class is named "\Aimeos\Client\Html\Locale\Select\Currency\Myname".
The name is case-sensitive and you should avoid camel case names like "MyName".


## param-name

Name of the parameter that contains the currency ID value

```
client/html/locale/select/currency/param-name = currency
```

* Default: currency
* Type: string - Parameter name for currency ID
* Since: 2015.06

Frameworks and applications normally use its own predefined parameter
that contains the current currency ID if they already support multiple
currencies. To adapt the Aimeos parameter name to the already used name,
you are able to configure it by using this setting.

See also:

* client/html/locale/select/language/param-name

## template-body

Relative path to the HTML body template of the locale select currency client.

```
client/html/locale/select/currency/template-body = locale/select/currency-body
```

* Default: locale/select/currency-body
* Type: string - Relative path to the template creating code for the HTML page body
* Since: 2014.09

The template file contains the HTML code and processing instructions
to generate the result shown in the body of the frontend. The
configuration string is the path to the template file relative
to the templates directory (usually in templates/client/html).

You can overwrite the template file configuration in extensions and
provide alternative templates. These alternative templates should be
named like the default one but suffixed by
an unique name. You may use the name of your project for this. If
you've implemented an alternative client class as well, it
should be suffixed by the name of the new class.

See also:

* client/html/locale/select/currency/template-header

## url/config

Associative list of configuration options used for generating the URL

```
client/html/locale/select/currency/url/config = Array
(
)
```

* Default: Array
(
)

* Type: string - Associative list of configuration options
* Since: 2014.09

You can specify additional options as key/value pairs used when generating
the URLs, like

```
 client/html/<clientname>/url/config = array( 'absoluteUri' => true )
```

The available key/value pairs depend on the application that embeds the e-commerce
framework. This is because the infrastructure of the application is used for
generating the URLs. The full list of available config options is referenced
in the "see also" section of this page.


# decorators
## excludes

Excludes decorators added by the "common" option from the locale select html client

```
client/html/locale/select/decorators/excludes = 
```

* Default: 
* Type: array - List of decorator names
* Since: 2014.05

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to remove a decorator added via
"client/html/common/decorators/default" before they are wrapped
around the html client.

```
 client/html/locale/select/decorators/excludes = array( 'decorator1' )
```

This would remove the decorator named "decorator1" from the list of
common decorators ("\Aimeos\Client\Html\Common\Decorator\*") added via
"client/html/common/decorators/default" to the html client.

See also:

* client/html/common/decorators/default
* client/html/locale/select/decorators/global
* client/html/locale/select/decorators/local

## global

Adds a list of globally available decorators only to the locale select html client

```
client/html/locale/select/decorators/global = 
```

* Default: 
* Type: array - List of decorator names
* Since: 2014.05

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap global decorators
("\Aimeos\Client\Html\Common\Decorator\*") around the html client.

```
 client/html/locale/select/decorators/global = array( 'decorator1' )
```

This would add the decorator named "decorator1" defined by
"\Aimeos\Client\Html\Common\Decorator\Decorator1" only to the html client.

See also:

* client/html/common/decorators/default
* client/html/locale/select/decorators/excludes
* client/html/locale/select/decorators/local

## local

Adds a list of local decorators only to the locale select html client

```
client/html/locale/select/decorators/local = 
```

* Default: 
* Type: array - List of decorator names
* Since: 2014.05

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap local decorators
("\Aimeos\Client\Html\Locale\Decorator\*") around the html client.

```
 client/html/locale/select/decorators/local = array( 'decorator2' )
```

This would add the decorator named "decorator2" defined by
"\Aimeos\Client\Html\Locale\Decorator\Decorator2" only to the html client.

See also:

* client/html/common/decorators/default
* client/html/locale/select/decorators/excludes
* client/html/locale/select/decorators/global

# language
## decorators/global

```
client/html/locale/select/language/decorators/global = Array
(
)
```

* Default: Array
(
)



## decorators/local

```
client/html/locale/select/language/decorators/local = Array
(
)
```

* Default: Array
(
)



## name

Name of the language part used by the locale selector client implementation

```
client/html/locale/select/language/name = Standard
```

* Default: Standard
* Type: string - Last part of the client class name
* Since: 2014.09

Use "Myname" if your class is named "\Aimeos\Client\Html\Locale\Select\Language\Myname".
The name is case-sensitive and you should avoid camel case names like "MyName".


## param-name

Name of the parameter that contains the language ID value

```
client/html/locale/select/language/param-name = locale
```

* Default: locale
* Type: string - Parameter name for language ID
* Since: 2015.06

Frameworks and applications normally use its own predefined parameter
that contains the current language ID if they are multi-language
capable. To adapt the Aimeos parameter name to the already used name,
you are able to configure it by using this setting.

See also:

* client/html/locale/select/currency/param-name

## template-body

Relative path to the HTML body template of the locale select language client.

```
client/html/locale/select/language/template-body = locale/select/language-body
```

* Default: locale/select/language-body
* Type: string - Relative path to the template creating code for the HTML page body
* Since: 2014.09

The template file contains the HTML code and processing instructions
to generate the result shown in the body of the frontend. The
configuration string is the path to the template file relative
to the templates directory (usually in templates/client/html).

You can overwrite the template file configuration in extensions and
provide alternative templates. These alternative templates should be
named like the default one but suffixed by
an unique name. You may use the name of your project for this. If
you've implemented an alternative client class as well, it
should be suffixed by the name of the new class.

See also:

* client/html/locale/select/language/template-header

## url/config

Associative list of configuration options used for generating the URL

```
client/html/locale/select/language/url/config = Array
(
)
```

* Default: Array
(
)

* Type: string - Associative list of configuration options
* Since: 2014.09

You can specify additional options as key/value pairs used when generating
the URLs, like

```
 client/html/<clientname>/url/config = array( 'absoluteUri' => true )
```

The available key/value pairs depend on the application that embeds the e-commerce
framework. This is because the infrastructure of the application is used for
generating the URLs. The full list of available config options is referenced
in the "see also" section of this page.


# name

Class name of the used locale select client implementation

```
client/html/locale/select/name = 
```

* Default: 
* Type: string - Last part of the class name
* Since: 2014.03

Each default HTML client can be replace by an alternative imlementation.
To use this implementation, you have to set the last part of the class
name as configuration value so the client factory knows which class it
has to instantiate.

For example, if the name of the default class is

```
 \Aimeos\Client\Html\Locale\Select\Standard
```

and you want to replace it with your own version named

```
 \Aimeos\Client\Html\Locale\Select\Myselect
```

then you have to set the this configuration option:

```
 client/html/locale/select/name = Myselect
```

The value is the last part of your own class name and it's case sensitive,
so take care that the configuration value is exactly named like the last
part of the class name.

The allowed characters of the class name are A-Z, a-z and 0-9. No other
characters are possible! You should always start the last part of the class
name with an upper case character and continue only with lower case characters
or numbers. Avoid chamel case names like "MySelect"!


# subparts

List of HTML sub-clients rendered within the locale select section

```
client/html/locale/select/subparts = Array
(
    [0] => language
    [1] => currency
)
```

* Default: Array
(
    [0] => language
    [1] => currency
)

* Type: array - List of sub-client names
* Since: 2014.09

The output of the frontend is composed of the code generated by the HTML
clients. Each HTML client can consist of serveral (or none) sub-clients
that are responsible for rendering certain sub-parts of the output. The
sub-clients can contain HTML clients themselves and therefore a
hierarchical tree of HTML clients is composed. Each HTML client creates
the output that is placed inside the container of its parent.

At first, always the HTML code generated by the parent is printed, then
the HTML code of its sub-clients. The order of the HTML sub-clients
determines the order of the output of these sub-clients inside the parent
container. If the configured list of clients is

```
 array( "subclient1", "subclient2" )
```

you can easily change the order of the output by reordering the subparts:

```
 client/html/<clients>/subparts = array( "subclient1", "subclient2" )
```

You can also remove one or more parts if they shouldn't be rendered:

```
 client/html/<clients>/subparts = array( "subclient1" )
```

As the clients only generates structural HTML, the layout defined via CSS
should support adding, removing or reordering content by a fluid like
design.


# template-body

Relative path to the HTML body template of the locale select client.

```
client/html/locale/select/template-body = locale/select/body
```

* Default: locale/select/body
* Type: string - Relative path to the template creating code for the HTML page body
* Since: 2014.09

The template file contains the HTML code and processing instructions
to generate the result shown in the body of the frontend. The
configuration string is the path to the template file relative
to the templates directory (usually in templates/client/html).

You can overwrite the template file configuration in extensions and
provide alternative templates. These alternative templates should be
named like the default one but suffixed by
an unique name. You may use the name of your project for this. If
you've implemented an alternative client class as well, it
should be suffixed by the name of the new class.

See also:

* client/html/locale/select/template-header

# template-header

Relative path to the HTML header template of the locale select client.

```
client/html/locale/select/template-header = locale/select/header
```

* Default: locale/select/header
* Type: string - Relative path to the template creating code for the HTML page head
* Since: 2014.09

The template file contains the HTML code and processing instructions
to generate the HTML code that is inserted into the HTML page header
of the rendered page in the frontend. The configuration string is the
path to the template file relative to the templates directory (usually
in templates/client/html).

You can overwrite the template file configuration in extensions and
provide alternative templates. These alternative templates should be
named like the default one but suffixed by
an unique name. You may use the name of your project for this. If
you've implemented an alternative client class as well, it
should be suffixed by the name of the new class.

See also:

* client/html/locale/select/template-body
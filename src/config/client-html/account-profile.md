
# domains

A list of domain names whose items should be available in the account profile view template

```
client/html/account/profile/domains = Array
(
    [0] => customer/address
)
```

* Default: Array
(
    [0] => customer/address
)

* Type: array - List of domain names
* Since: 2016.10

The templates rendering customer details can contain additional
items. If you want to display additional content, you can configure
your own list of domains (attribute, media, price, product, text,
etc. are domains) whose items are fetched from the storage.


# name

Class name of the used account profile client implementation

```
client/html/account/profile/name = 
```

* Default: 
* Type: string - Last part of the class name
* Since: 2016.10

Each default HTML client can be replace by an alternative imlementation.
To use this implementation, you have to set the last part of the class
name as configuration value so the client factory knows which class it
has to instantiate.

For example, if the name of the default class is

```
 \Aimeos\Client\Html\Account\Profile\Standard
```

and you want to replace it with your own version named

```
 \Aimeos\Client\Html\Account\Profile\Myprofile
```

then you have to set the this configuration option:

```
 client/html/account/profile/name = Myprofile
```

The value is the last part of your own class name and it's case sensitive,
so take care that the configuration value is exactly named like the last
part of the class name.

The allowed characters of the class name are A-Z, a-z and 0-9. No other
characters are possible! You should always start the last part of the class
name with an upper case character and continue only with lower case characters
or numbers. Avoid chamel case names like "MyProfile"!


# template-body

Relative path to the HTML body template of the account profile client.

```
client/html/account/profile/template-body = 
```

* Default: 
* Type: string - Relative path to the template creating code for the HTML page body
* Since: 2016.10

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

* client/html/account/profile/template-header

# template-header

Relative path to the HTML header template of the account profile client.

```
client/html/account/profile/template-header = 
```

* Default: 
* Type: string - Relative path to the template creating code for the HTML page head
* Since: 2016.10

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

* client/html/account/profile/template-body

# url
## action

Name of the action that should create the output

```
client/html/account/profile/url/action = profile
```

* Default: profile
* Type: string - Name of the action
* Since: 2019.10

In Model-View-Controller (MVC) applications, actions are the methods of a
controller that create parts of the output displayed in the generated HTML page.
Action names are usually alpha-numeric.

See also:

* client/html/account/profile/url/target
* client/html/account/profile/url/controller
* client/html/account/profile/url/config

## config

Associative list of configuration options used for generating the URL

```
client/html/account/profile/url/config = Array
(
)
```

* Default: Array
(
)

* Type: string - Associative list of configuration options
* Since: 2019.10

You can specify additional options as key/value pairs used when generating
the URLs, like

```
 client/html/<clientname>/url/config = array( 'absoluteUri' => true )
```

The available key/value pairs depend on the application that embeds the e-commerce
framework. This is because the infrastructure of the application is used for
generating the URLs. The full list of available config options is referenced
in the "see also" section of this page.

See also:

* client/html/account/profile/url/target
* client/html/account/profile/url/controller
* client/html/account/profile/url/action
* client/html/url/config

## controller

Name of the controller whose action should be called

```
client/html/account/profile/url/controller = Account
```

* Default: Account
* Type: string - Name of the controller
* Since: 2019.10

In Model-View-Controller (MVC) applications, the controller contains the methods
that create parts of the output displayed in the generated HTML page. Controller
names are usually alpha-numeric.

See also:

* client/html/account/profile/url/target
* client/html/account/profile/url/action
* client/html/account/profile/url/config

## filter

Removes parameters for the detail page before generating the URL

```
client/html/account/profile/url/filter = Array
(
)
```

* Default: Array
(
)

* Type: array - List of parameter names to remove
* Since: 2019.10

For SEO, it's nice to have URLs which contains only required parameters.
This setting removes the listed parameters from the URLs. Keep care to
remove no required parameters!

See also:

* client/html/account/profile/url/target
* client/html/account/profile/url/controller
* client/html/account/profile/url/action
* client/html/account/profile/url/config

## target

Destination of the URL where the controller specified in the URL is known

```
client/html/account/profile/url/target = 
```

* Default: 
* Type: string - Destination of the URL
* Since: 2019.10

The destination can be a page ID like in a content management system or the
module of a software development framework. This "target" must contain or know
the controller that should be called by the generated URL.

See also:

* client/html/account/profile/url/controller
* client/html/account/profile/url/action
* client/html/account/profile/url/config
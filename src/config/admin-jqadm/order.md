
# actions

Actions available in the list view of the order panel

```
admin/jqadm/order/actions = Array
(
    [order-export] => order-export
)
```

* Default: 
```
Array
(
    [0] => order-export
)
```
* Type: array - List of action queue names
* Since: 2020.10

List of actions, the editor can select from in the list header of the order
panel. You can dynamically extend the available actions like exporting the
selected orders in CSV format and translate the action names using the
"admin/code" translation domain.

The action names will be passed as "queue" parameter to the export method
of the JQADM order class, which will create an entry for the message queue
from the selected filter criteria. You have to implement a suitable controller
which must fetch the entries from the message queue and generate the appropriate
files. If files should be offered for download in the dashboard, a new job
entry must be created using the MAdmin Job manager.


# decorators
## excludes

Excludes decorators added by the "common" option from the order JQAdm client

```
admin/jqadm/order/decorators/excludes = 
```

* Type: array - List of decorator names
* Since: 2016.01

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to remove a decorator added via
"client/jqadm/common/decorators/default" before they are wrapped
around the JQAdm client.

```
 admin/jqadm/order/decorators/excludes = array( 'decorator1' )
```

This would remove the decorator named "decorator1" from the list of
common decorators ("\Aimeos\Admin\JQAdm\Common\Decorator\*") added via
"client/jqadm/common/decorators/default" to the JQAdm client.

See also:

* admin/jqadm/common/decorators/default
* admin/jqadm/order/decorators/global
* admin/jqadm/order/decorators/local

## global

Adds a list of globally available decorators only to the order JQAdm client

```
admin/jqadm/order/decorators/global = 
```

* Type: array - List of decorator names
* Since: 2016.01

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap global decorators
("\Aimeos\Admin\JQAdm\Common\Decorator\*") around the JQAdm client.

```
 admin/jqadm/order/decorators/global = array( 'decorator1' )
```

This would add the decorator named "decorator1" defined by
"\Aimeos\Admin\JQAdm\Common\Decorator\Decorator1" only to the JQAdm client.

See also:

* admin/jqadm/common/decorators/default
* admin/jqadm/order/decorators/excludes
* admin/jqadm/order/decorators/local

## local

Adds a list of local decorators only to the order JQAdm client

```
admin/jqadm/order/decorators/local = 
```

* Type: array - List of decorator names
* Since: 2016.01

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap local decorators
("\Aimeos\Admin\JQAdm\Order\Decorator\*") around the JQAdm client.

```
 admin/jqadm/order/decorators/local = array( 'decorator2' )
```

This would add the decorator named "decorator2" defined by
"\Aimeos\Admin\JQAdm\Order\Decorator\Decorator2" only to the JQAdm client.

See also:

* admin/jqadm/common/decorators/default
* admin/jqadm/order/decorators/excludes
* admin/jqadm/order/decorators/global

# fields

List of order columns that should be displayed in the list view

```
admin/jqadm/order/fields = Array
(
    [0] => order.invoiceno
    [1] => order.ctime
    [2] => order.statuspayment
    [3] => order.address.lastname
)
```

* Default: 
```
Array
(
    [0] => order.invoiceno
    [1] => order.ctime
    [2] => order.statuspayment
    [3] => order.address.lastname
)
```
* Type: array - List of field names, i.e. search keys
* Since: 2017.07

Changes the list of order columns shown by default in the order list view.
The columns can be changed by the editor as required within the administraiton
interface.

The names of the colums are in fact the search keys defined by the managers,
e.g. "order.id" for the order ID.


# name

Class name of the used order panel implementation

```
admin/jqadm/order/name = 
```

* Type: string - Last part of the class name
* Since: 2016.01

Each default admin client can be replace by an alternative imlementation.
To use this implementation, you have to set the last part of the class
name as configuration value so the client factory knows which class it
has to instantiate.

For example, if the name of the default class is

```
 \Aimeos\Admin\JQAdm\Order\Standard
```

and you want to replace it with your own version named

```
 \Aimeos\Admin\JQAdm\Order\Myfavorite
```

then you have to set the this configuration option:

```
 admin/jqadm/order/name = Myfavorite
```

The value is the last part of your own class name and it's case sensitive,
so take care that the configuration value is exactly named like the last
part of the class name.

The allowed characters of the class name are A-Z, a-z and 0-9. No other
characters are possible! You should always start the last part of the class
name with an upper case character and continue only with lower case characters
or numbers. Avoid chamel case names like "MyFavorite"!


# service
## delivery/attribute/suggest

List of suggested configuration keys for delivery service attributes in orders

```
admin/jqadm/order/service/delivery/attribute/suggest = Array
(
    [0] => trackingid
)
```

* Default: 
```
Array
(
    [0] => trackingid
)
```
* Type: string - List of suggested config keys
* Since: 2017.10

Service attributes in orders can store arbitrary key value pairs. This
setting gives editors a hint which config keys are available and are used
in the templates.

See also:

* admin/jqadm/order/service/payment/attribute/suggest

## payment/attribute/suggest

List of suggested configuration keys for payment service attributes in orders

```
admin/jqadm/order/service/payment/attribute/suggest = Array
(
)
```

* Default: 
```
Array
(
)
```
* Type: string - List of suggested config keys
* Since: 2017.10

Service attributes in orders can store arbitrary key value pairs. This
setting gives editors a hint which config keys are available and are used
in the templates.

See also:

* admin/jqadm/order/service/delivery/attribute/suggest

# subparts

List of JQAdm sub-clients rendered within the order section

```
admin/jqadm/order/subparts = Array
(
    [transaction] => transaction
)
```

* Default: 
```
Array
(
)
```
* Type: array - List of sub-client names
* Since: 2016.01

The output of the frontend is composed of the code generated by the JQAdm
clients. Each JQAdm client can consist of serveral (or none) sub-clients
that are responsible for rendering certain sub-parts of the output. The
sub-clients can contain JQAdm clients themselves and therefore a
hierarchical tree of JQAdm clients is composed. Each JQAdm client creates
the output that is placed inside the container of its parent.

At first, always the JQAdm code generated by the parent is printed, then
the JQAdm code of its sub-clients. The order of the JQAdm sub-clients
determines the order of the output of these sub-clients inside the parent
container. If the configured list of clients is

```
 array( "subclient1", "subclient2" )
```

you can easily change the order of the output by reordering the subparts:

```
 admin/jqadm/<clients>/subparts = array( "subclient1", "subclient2" )
```

You can also remove one or more parts if they shouldn't be rendered:

```
 admin/jqadm/<clients>/subparts = array( "subclient1" )
```

As the clients only generates structural JQAdm, the layout defined via CSS
should support adding, removing or reordering content by a fluid like
design.


# template-item

Relative path to the HTML body template for the order item.

```
admin/jqadm/order/template-item = order/item
```

* Default: `order/item`
* Type: string - Relative path to the template creating the HTML code
* Since: 2016.04

The template file contains the HTML code and processing instructions
to generate the result shown in the body of the frontend. The
configuration string is the path to the template file relative
to the templates directory (usually in templates/admin/jqadm).

You can overwrite the template file configuration in extensions and
provide alternative templates. These alternative templates should be
named like the default one but with the string "default" replaced by
an unique name. You may use the name of your project for this. If
you've implemented an alternative client class as well, "default"
should be replaced by the name of the new class.


# template-list

Relative path to the HTML body template for the order list.

```
admin/jqadm/order/template-list = order/list
```

* Default: `order/list`
* Type: string - Relative path to the template creating the HTML code
* Since: 2016.04

The template file contains the HTML code and processing instructions
to generate the result shown in the body of the frontend. The
configuration string is the path to the template file relative
to the templates directory (usually in templates/admin/jqadm).

You can overwrite the template file configuration in extensions and
provide alternative templates. These alternative templates should be
named like the default one but with the string "default" replaced by
an unique name. You may use the name of your project for this. If
you've implemented an alternative client class as well, "default"
should be replaced by the name of the new class.


# transaction
## decorators/excludes

Excludes decorators added by the "common" option from the order JQAdm client

```
admin/jqadm/order/transaction/decorators/excludes = 
```

* Type: array - List of decorator names
* Since: 2023.01

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to remove a decorator added via
"admin/jqadm/common/decorators/default" before they are wrapped
around the JQAdm client.

```
 admin/jqadm/order/transaction/decorators/excludes = array( 'decorator1' )
```

This would remove the decorator named "decorator1" from the list of
common decorators ("\Aimeos\Admin\JQAdm\Common\Decorator\*") added via
"admin/jqadm/common/decorators/default" to the JQAdm client.

See also:

* admin/jqadm/common/decorators/default
* admin/jqadm/order/transaction/decorators/global
* admin/jqadm/order/transaction/decorators/local

## decorators/global

Adds a list of globally available decorators only to the order JQAdm client

```
admin/jqadm/order/transaction/decorators/global = Array
(
)
```

* Default: 
```
Array
(
)
```
* Type: array - List of decorator names
* Since: 2023.01

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap global decorators
("\Aimeos\Admin\JQAdm\Common\Decorator\*") around the JQAdm client.

```
 admin/jqadm/order/transaction/decorators/global = array( 'decorator1' )
```

This would add the decorator named "decorator1" defined by
"\Aimeos\Admin\JQAdm\Common\Decorator\Decorator1" only to the JQAdm client.

See also:

* admin/jqadm/common/decorators/default
* admin/jqadm/order/transaction/decorators/excludes
* admin/jqadm/order/transaction/decorators/local

## decorators/local

Adds a list of local decorators only to the order JQAdm client

```
admin/jqadm/order/transaction/decorators/local = Array
(
)
```

* Default: 
```
Array
(
)
```
* Type: array - List of decorator names
* Since: 2023.01

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap local decorators
("\Aimeos\Admin\JQAdm\Order\Decorator\*") around the JQAdm client.

```
 admin/jqadm/order/transaction/decorators/local = array( 'decorator2' )
```

This would add the decorator named "decorator2" defined by
"\Aimeos\Admin\JQAdm\Order\Decorator\Decorator2" only to the JQAdm client.

See also:

* admin/jqadm/common/decorators/default
* admin/jqadm/order/transaction/decorators/excludes
* admin/jqadm/order/transaction/decorators/global

## name

Name of the transaction subpart used by the JQAdm order implementation

```
admin/jqadm/order/transaction/name = Standard
```

* Default: `Standard`
* Type: string - Last part of the JQAdm class name
* Since: 2023.01

Use "Myname" if your class is named "\Aimeos\Admin\Jqadm\Order\Transaction\Myname".
The name is case-sensitive and you should avoid camel case names like "MyName".


## subparts

List of JQAdm sub-clients rendered within the order transaction section

```
admin/jqadm/order/transaction/subparts = Array
(
)
```

* Default: 
```
Array
(
)
```
* Type: array - List of sub-client names
* Since: 2023.01

The output of the frontend is composed of the code generated by the JQAdm
clients. Each JQAdm client can consist of serveral (or none) sub-clients
that are responsible for rendering certain sub-parts of the output. The
sub-clients can contain JQAdm clients themselves and therefore a
hierarchical tree of JQAdm clients is composed. Each JQAdm client creates
the output that is placed inside the container of its parent.

At first, always the JQAdm code generated by the parent is printed, then
the JQAdm code of its sub-clients. The transaction of the JQAdm sub-clients
determines the transaction of the output of these sub-clients inside the parent
container. If the configured list of clients is

```
 array( "subclient1", "subclient2" )
```

you can easily change the transaction of the output by retransactioning the subparts:

```
 admin/jqadm/<clients>/subparts = array( "subclient1", "subclient2" )
```

You can also remove one or more parts if they shouldn't be rendered:

```
 admin/jqadm/<clients>/subparts = array( "subclient1" )
```

As the clients only generates structural JQAdm, the layout defined via CSS
should support adding, removing or retransactioning content by a fluid like
design.


## template-item

Relative path to the HTML body template of the transaction subpart for orders.

```
admin/jqadm/order/transaction/template-item = order/item-transaction
```

* Default: `order/item-transaction`
* Type: string - Relative path to the template creating the HTML code
* Since: 2016.04

The template file contains the HTML code and processing instructions
to generate the result shown in the body of the frontend. The
configuration string is the path to the template file relative
to the templates directory (usually in templates/admin/jqadm).

You can overwrite the template file configuration in extensions and
provide alternative templates. These alternative templates should be
named like the default one but with the string "default" replaced by
an unique name. You may use the name of your project for this. If
you've implemented an alternative client class as well, "default"
should be replaced by the name of the new class.

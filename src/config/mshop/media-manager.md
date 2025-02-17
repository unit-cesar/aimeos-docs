
# count
## ansi

Counts the number of records matched by the given criteria in the database

```
mshop/media/manager/count/ansi = 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mmed."id"
 	FROM "mshop_media" mmed
 	:joins
 	WHERE :cond
 	GROUP BY mmed."id"
 	ORDER BY mmed."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list
```

* Default: mshop/media/manager/count
* Type: string - SQL statement for counting items
* Since: 2014.03

Counts all records matched by the given criteria from the media
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the statement can count all records from the
current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

Both, the strings for ":joins" and for ":cond" are the same as for
the "search" SQL statement.

Contrary to the "search" statement, it doesn't return any records
but instead the number of records that have been found. As counting
thousands of records can be a long running task, the maximum number
of counted records is limited for performance reasons.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/insert/ansi
* mshop/media/manager/update/ansi
* mshop/media/manager/newid/ansi
* mshop/media/manager/delete/ansi
* mshop/media/manager/search/ansi

## mysql

Counts the number of records matched by the given criteria in the database

```
mshop/media/manager/count/mysql = 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mmed."id"
 	FROM "mshop_media" mmed
 	:joins
 	WHERE :cond
 	GROUP BY mmed."id"
 	ORDER BY mmed."id"
 	LIMIT 10000 OFFSET 0
 ) AS list
```

* Default: 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mmed."id"
 	FROM "mshop_media" mmed
 	:joins
 	WHERE :cond
 	GROUP BY mmed."id"
 	ORDER BY mmed."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list


See also:

* mshop/media/manager/count/ansi

# decorators
## excludes

Excludes decorators added by the "common" option from the media manager

```
mshop/media/manager/decorators/excludes = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to remove a decorator added via
"mshop/common/manager/decorators/default" before they are wrapped
around the media manager.

```
 mshop/media/manager/decorators/excludes = array( 'decorator1' )
```

This would remove the decorator named "decorator1" from the list of
common decorators ("\Aimeos\MShop\Common\Manager\Decorator\*") added via
"mshop/common/manager/decorators/default" for the media manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/decorators/global
* mshop/media/manager/decorators/local

## global

Adds a list of globally available decorators only to the media manager

```
mshop/media/manager/decorators/global = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap global decorators
("\Aimeos\MShop\Common\Manager\Decorator\*") around the media manager.

```
 mshop/media/manager/decorators/global = array( 'decorator1' )
```

This would add the decorator named "decorator1" defined by
"\Aimeos\MShop\Common\Manager\Decorator\Decorator1" only to the media
manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/decorators/excludes
* mshop/media/manager/decorators/local

## local

Adds a list of local decorators only to the media manager

```
mshop/media/manager/decorators/local = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap local decorators
("\Aimeos\MShop\Media\Manager\Decorator\*") around the media manager.

```
 mshop/media/manager/decorators/local = array( 'decorator2' )
```

This would add the decorator named "decorator2" defined by
"\Aimeos\MShop\Media\Manager\Decorator\Decorator2" only to the media
manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/decorators/excludes
* mshop/media/manager/decorators/global

# delete
## ansi

Deletes the items matched by the given IDs from the database

```
mshop/media/manager/delete/ansi = 
 DELETE FROM "mshop_media"
 WHERE :cond AND "siteid" LIKE ?
```

* Default: mshop/media/manager/delete
* Type: string - SQL statement for deleting items
* Since: 2014.03

Removes the records specified by the given IDs from the media database.
The records must be from the site that is configured via the
context item.

The ":cond" placeholder is replaced by the name of the ID column and
the given ID or list of IDs while the site ID is bound to the question
mark.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/insert/ansi
* mshop/media/manager/update/ansi
* mshop/media/manager/newid/ansi
* mshop/media/manager/search/ansi
* mshop/media/manager/count/ansi

## mysql

Deletes the items matched by the given IDs from the database

```
mshop/media/manager/delete/mysql = 
 DELETE FROM "mshop_media"
 WHERE :cond AND "siteid" LIKE ?
```

* Default: 
 DELETE FROM "mshop_media"
 WHERE :cond AND "siteid" LIKE ?


See also:

* mshop/media/manager/delete/ansi

# insert
## ansi

Inserts a new media record into the database table

```
mshop/media/manager/insert/ansi = 
 INSERT INTO "mshop_media" ( :names
 	"langid", "type", "label", "mimetype", "link", "status", "fsname",
 	"domain", "preview", "mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?
 )
```

* Default: mshop/media/manager/insert
* Type: string - SQL statement for inserting records
* Since: 2014.03

Items with no ID yet (i.e. the ID is NULL) will be created in
the database and the newly created ID retrieved afterwards
using the "newid" SQL statement.

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the media item to the statement before they are
sent to the database server. The number of question marks must
be the same as the number of columns listed in the INSERT
statement. The order of the columns must correspond to the
order in the save() method, so the correct values are
bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/update/ansi
* mshop/media/manager/newid/ansi
* mshop/media/manager/delete/ansi
* mshop/media/manager/search/ansi
* mshop/media/manager/count/ansi

## mysql

Inserts a new media record into the database table

```
mshop/media/manager/insert/mysql = 
 INSERT INTO "mshop_media" ( :names
 	"langid", "type", "label", "mimetype", "link", "status", "fsname",
 	"domain", "preview", "mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?
 )
```

* Default: 
 INSERT INTO "mshop_media" ( :names
 	"langid", "type", "label", "mimetype", "link", "status", "fsname",
 	"domain", "preview", "mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?
 )


See also:

* mshop/media/manager/insert/ansi

# lists
## aggregate/ansi

Counts the number of records grouped by the values in the key column and matched by the given criteria

```
mshop/media/manager/lists/aggregate/ansi = 
 SELECT :keys, :type("val") AS "value"
 FROM (
 	SELECT :acols, :val AS "val"
 	FROM "mshop_media_list" mmedli
 	:joins
 	WHERE :cond
 	GROUP BY :cols, mmedli."id"
 	ORDER BY :order
 	OFFSET :start ROWS FETCH NEXT :size ROWS ONLY
 ) AS list
 GROUP BY :keys
```

* Default: mshop/media/manager/lists/aggregate
* Type: string - SQL statement for aggregating order items
* Since: 2014.07

Groups all records by the values in the key column and counts their
occurence. The matched records can be limited by the given criteria
from the order database. The records must be from one of the sites
that are configured via the context item. If the current site is part
of a tree of sites, the statement can count all records from the
current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

This statement doesn't return any records. Instead, it returns pairs
of the different values found in the key column together with the
number of records that have been found for that key values.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/lists/insert/ansi
* mshop/media/manager/lists/update/ansi
* mshop/media/manager/lists/newid/ansi
* mshop/media/manager/lists/delete/ansi
* mshop/media/manager/lists/search/ansi
* mshop/media/manager/lists/count/ansi

## aggregate/mysql

Counts the number of records grouped by the values in the key column and matched by the given criteria

```
mshop/media/manager/lists/aggregate/mysql = 
 SELECT :keys, :type("val") AS "value"
 FROM (
 	SELECT :acols, :val AS "val"
 	FROM "mshop_media_list" mmedli
 	:joins
 	WHERE :cond
 	GROUP BY :cols, mmedli."id"
 	ORDER BY :order
 	LIMIT :size OFFSET :start
 ) AS list
 GROUP BY :keys
```

* Default: 
 SELECT :keys, :type("val") AS "value"
 FROM (
 	SELECT :acols, :val AS "val"
 	FROM "mshop_media_list" mmedli
 	:joins
 	WHERE :cond
 	GROUP BY :cols, mmedli."id"
 	ORDER BY :order
 	OFFSET :start ROWS FETCH NEXT :size ROWS ONLY
 ) AS list
 GROUP BY :keys


See also:

* mshop/media/manager/lists/aggregate/ansi

## count/ansi

Counts the number of records matched by the given criteria in the database

```
mshop/media/manager/lists/count/ansi = 
 SELECT COUNT(*) AS "count"
 FROM(
 	SELECT mmedli."id"
 	FROM "mshop_media_list" mmedli
 	:joins
 	WHERE :cond
 	ORDER BY mmedli."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list
```

* Default: mshop/media/manager/lists/count
* Type: string - SQL statement for counting items
* Since: 2014.03

Counts all records matched by the given criteria from the media
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the statement can count all records from the
current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

Both, the strings for ":joins" and for ":cond" are the same as for
the "search" SQL statement.

Contrary to the "search" statement, it doesn't return any records
but instead the number of records that have been found. As counting
thousands of records can be a long running task, the maximum number
of counted records is limited for performance reasons.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/lists/insert/ansi
* mshop/media/manager/lists/update/ansi
* mshop/media/manager/lists/newid/ansi
* mshop/media/manager/lists/delete/ansi
* mshop/media/manager/lists/search/ansi
* mshop/media/manager/lists/aggregate/ansi

## count/mysql

Counts the number of records matched by the given criteria in the database

```
mshop/media/manager/lists/count/mysql = 
 SELECT COUNT(*) AS "count"
 FROM(
 	SELECT mmedli."id"
 	FROM "mshop_media_list" mmedli
 	:joins
 	WHERE :cond
 	ORDER BY mmedli."id"
 	LIMIT 10000 OFFSET 0
 ) AS list
```

* Default: 
 SELECT COUNT(*) AS "count"
 FROM(
 	SELECT mmedli."id"
 	FROM "mshop_media_list" mmedli
 	:joins
 	WHERE :cond
 	ORDER BY mmedli."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list


See also:

* mshop/media/manager/lists/count/ansi

## decorators/excludes

Excludes decorators added by the "common" option from the media list manager

```
mshop/media/manager/lists/decorators/excludes = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to remove a decorator added via
"mshop/common/manager/decorators/default" before they are wrapped
around the media list manager.

```
 mshop/media/manager/lists/decorators/excludes = array( 'decorator1' )
```

This would remove the decorator named "decorator1" from the list of
common decorators ("\Aimeos\MShop\Common\Manager\Decorator\*") added via
"mshop/common/manager/decorators/default" for the media list manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/lists/decorators/global
* mshop/media/manager/lists/decorators/local

## decorators/global

Adds a list of globally available decorators only to the media list manager

```
mshop/media/manager/lists/decorators/global = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap global decorators
("\Aimeos\MShop\Common\Manager\Decorator\*") around the media list
manager.

```
 mshop/media/manager/lists/decorators/global = array( 'decorator1' )
```

This would add the decorator named "decorator1" defined by
"\Aimeos\MShop\Common\Manager\Decorator\Decorator1" only to the media
list manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/lists/decorators/excludes
* mshop/media/manager/lists/decorators/local

## decorators/local

Adds a list of local decorators only to the media list manager

```
mshop/media/manager/lists/decorators/local = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap local decorators
("\Aimeos\MShop\Media\Manager\Lists\Decorator\*") around the media list
manager.

```
 mshop/media/manager/lists/decorators/local = array( 'decorator2' )
```

This would add the decorator named "decorator2" defined by
"\Aimeos\MShop\Media\Manager\Lists\Decorator\Decorator2" only to the
media list manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/lists/decorators/excludes
* mshop/media/manager/lists/decorators/global

## delete/ansi

Deletes the items matched by the given IDs from the database

```
mshop/media/manager/lists/delete/ansi = 
 DELETE FROM "mshop_media_list"
 WHERE :cond AND "siteid" LIKE ?
```

* Default: mshop/media/manager/lists/delete
* Type: string - SQL statement for deleting items
* Since: 2014.03

Removes the records specified by the given IDs from the media database.
The records must be from the site that is configured via the
context item.

The ":cond" placeholder is replaced by the name of the ID column and
the given ID or list of IDs while the site ID is bound to the question
mark.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/lists/insert/ansi
* mshop/media/manager/lists/update/ansi
* mshop/media/manager/lists/newid/ansi
* mshop/media/manager/lists/search/ansi
* mshop/media/manager/lists/count/ansi
* mshop/media/manager/lists/aggregate/ansi

## delete/mysql

Deletes the items matched by the given IDs from the database

```
mshop/media/manager/lists/delete/mysql = 
 DELETE FROM "mshop_media_list"
 WHERE :cond AND "siteid" LIKE ?
```

* Default: 
 DELETE FROM "mshop_media_list"
 WHERE :cond AND "siteid" LIKE ?


See also:

* mshop/media/manager/lists/delete/ansi

## insert/ansi

Inserts a new media list record into the database table

```
mshop/media/manager/lists/insert/ansi = 
 INSERT INTO "mshop_media_list" ( :names
 	"parentid", "key", "type", "domain", "refid", "start", "end",
 	"config", "pos", "status", "mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?
 )
```

* Default: mshop/media/manager/lists/insert
* Type: string - SQL statement for inserting records
* Since: 2014.03

Items with no ID yet (i.e. the ID is NULL) will be created in
the database and the newly created ID retrieved afterwards
using the "newid" SQL statement.

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the media list item to the statement before they are
sent to the database server. The number of question marks must
be the same as the number of columns listed in the INSERT
statement. The order of the columns must correspond to the
order in the save() method, so the correct values are
bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/lists/update/ansi
* mshop/media/manager/lists/newid/ansi
* mshop/media/manager/lists/delete/ansi
* mshop/media/manager/lists/search/ansi
* mshop/media/manager/lists/count/ansi
* mshop/media/manager/lists/aggregate/ansi

## insert/mysql

Inserts a new media list record into the database table

```
mshop/media/manager/lists/insert/mysql = 
 INSERT INTO "mshop_media_list" ( :names
 	"parentid", "key", "type", "domain", "refid", "start", "end",
 	"config", "pos", "status", "mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?
 )
```

* Default: 
 INSERT INTO "mshop_media_list" ( :names
 	"parentid", "key", "type", "domain", "refid", "start", "end",
 	"config", "pos", "status", "mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?
 )


See also:

* mshop/media/manager/lists/insert/ansi

## name

Class name of the used media list manager implementation

```
mshop/media/manager/lists/name = Standard
```

* Default: Standard
* Type: string - Last part of the class name
* Since: 2014.03

Each default media list manager can be replaced by an alternative imlementation.
To use this implementation, you have to set the last part of the class
name as configuration value so the manager factory knows which class it
has to instantiate.

For example, if the name of the default class is

```
 \Aimeos\MShop\Media\Manager\Lists\Standard
```

and you want to replace it with your own version named

```
 \Aimeos\MShop\Media\Manager\Lists\Mylist
```

then you have to set the this configuration option:

```
 mshop/media/manager/lists/name = Mylist
```

The value is the last part of your own class name and it's case sensitive,
so take care that the configuration value is exactly named like the last
part of the class name.

The allowed characters of the class name are A-Z, a-z and 0-9. No other
characters are possible! You should always start the last part of the class
name with an upper case character and continue only with lower case characters
or numbers. Avoid chamel case names like "MyList"!


## newid/ansi

Retrieves the ID generated by the database when inserting a new record

```
mshop/media/manager/lists/newid/ansi = mshop/media/manager/lists/newid
```

* Default: mshop/media/manager/lists/newid
* Type: string - SQL statement for retrieving the last inserted record ID
* Since: 2014.03

As soon as a new record is inserted into the database table,
the database server generates a new and unique identifier for
that record. This ID can be used for retrieving, updating and
deleting that specific record from the table again.

For MySQL:
```
 SELECT LAST_INSERT_ID()
For PostgreSQL:
 SELECT currval('seq_mmedli_id')
For SQL Server:
 SELECT SCOPE_IDENTITY()
For Oracle:
 SELECT "seq_mmedli_id".CURRVAL FROM DUAL
```

There's no way to retrive the new ID by a SQL statements that
fits for most database servers as they implement their own
specific way.

See also:

* mshop/media/manager/lists/insert/ansi
* mshop/media/manager/lists/update/ansi
* mshop/media/manager/lists/delete/ansi
* mshop/media/manager/lists/search/ansi
* mshop/media/manager/lists/count/ansi
* mshop/media/manager/lists/aggregate/ansi

## newid/mysql

Retrieves the ID generated by the database when inserting a new record

```
mshop/media/manager/lists/newid/mysql = SELECT LAST_INSERT_ID()
```

* Default: mshop/media/manager/lists/newid

See also:

* mshop/media/manager/lists/newid/ansi

## search/ansi

Retrieves the records matched by the given criteria in the database

```
mshop/media/manager/lists/search/ansi = 
 SELECT :columns
 	mmedli."id" AS "media.lists.id", mmedli."parentid" AS "media.lists.parentid",
 	mmedli."siteid" AS "media.lists.siteid", mmedli."type" AS "media.lists.type",
 	mmedli."domain" AS "media.lists.domain", mmedli."refid" AS "media.lists.refid",
 	mmedli."start" AS "media.lists.datestart", mmedli."end" AS "media.lists.dateend",
 	mmedli."config" AS "media.lists.config", mmedli."pos" AS "media.lists.position",
 	mmedli."status" AS "media.lists.status", mmedli."mtime" AS "media.lists.mtime",
 	mmedli."editor" AS "media.lists.editor", mmedli."ctime" AS "media.lists.ctime"
 FROM "mshop_media_list" mmedli
 :joins
 WHERE :cond
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY
```

* Default: mshop/media/manager/lists/search
* Type: string - SQL statement for searching items
* Since: 2014.03

Fetches the records matched by the given criteria from the media
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the SELECT statement can retrieve all records
from the current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

If the records that are retrieved should be ordered by one or more
columns, the generated string of column / sort direction pairs
replaces the ":order" placeholder. In case no ordering is required,
the complete ORDER BY part including the "/*-orderby*/.../*orderby-*/"
markers is removed to speed up retrieving the records. Columns of
sub-managers can also be used for ordering the result set but then
no index can be used.

The number of returned records can be limited and can start at any
number between the begining and the end of the result set. For that
the ":size" and ":start" placeholders are replaced by the
corresponding values from the criteria object. The default values
are 0 for the start and 100 for the size value.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/lists/insert/ansi
* mshop/media/manager/lists/update/ansi
* mshop/media/manager/lists/newid/ansi
* mshop/media/manager/lists/delete/ansi
* mshop/media/manager/lists/count/ansi
* mshop/media/manager/lists/aggregate/ansi

## search/mysql

Retrieves the records matched by the given criteria in the database

```
mshop/media/manager/lists/search/mysql = 
 SELECT :columns
 	mmedli."id" AS "media.lists.id", mmedli."parentid" AS "media.lists.parentid",
 	mmedli."siteid" AS "media.lists.siteid", mmedli."type" AS "media.lists.type",
 	mmedli."domain" AS "media.lists.domain", mmedli."refid" AS "media.lists.refid",
 	mmedli."start" AS "media.lists.datestart", mmedli."end" AS "media.lists.dateend",
 	mmedli."config" AS "media.lists.config", mmedli."pos" AS "media.lists.position",
 	mmedli."status" AS "media.lists.status", mmedli."mtime" AS "media.lists.mtime",
 	mmedli."editor" AS "media.lists.editor", mmedli."ctime" AS "media.lists.ctime"
 FROM "mshop_media_list" mmedli
 :joins
 WHERE :cond
 ORDER BY :order
 LIMIT :size OFFSET :start
```

* Default: 
 SELECT :columns
 	mmedli."id" AS "media.lists.id", mmedli."parentid" AS "media.lists.parentid",
 	mmedli."siteid" AS "media.lists.siteid", mmedli."type" AS "media.lists.type",
 	mmedli."domain" AS "media.lists.domain", mmedli."refid" AS "media.lists.refid",
 	mmedli."start" AS "media.lists.datestart", mmedli."end" AS "media.lists.dateend",
 	mmedli."config" AS "media.lists.config", mmedli."pos" AS "media.lists.position",
 	mmedli."status" AS "media.lists.status", mmedli."mtime" AS "media.lists.mtime",
 	mmedli."editor" AS "media.lists.editor", mmedli."ctime" AS "media.lists.ctime"
 FROM "mshop_media_list" mmedli
 :joins
 WHERE :cond
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY


See also:

* mshop/media/manager/lists/search/ansi

## submanagers

List of manager names that can be instantiated by the media list manager

```
mshop/media/manager/lists/submanagers = Array
(
)
```

* Default: Array
(
)

* Type: array - List of sub-manager names
* Since: 2014.03

Managers provide a generic interface to the underlying storage.
Each manager has or can have sub-managers caring about particular
aspects. Each of these sub-managers can be instantiated by its
parent manager using the getSubManager() method.

The search keys from sub-managers can be normally used in the
manager as well. It allows you to search for items of the manager
using the search keys of the sub-managers to further limit the
retrieved list of items.


## type/count/ansi

Counts the number of records matched by the given criteria in the database

```
mshop/media/manager/lists/type/count/ansi = 
 SELECT COUNT(*) AS "count"
 FROM(
 	SELECT mmedlity."id"
 	FROM "mshop_media_list_type" mmedlity
 	:joins
 	WHERE :cond
 	ORDER BY mmedlity."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list
```

* Default: mshop/media/manager/lists/type/count
* Type: string - SQL statement for counting items
* Since: 2014.03

Counts all records matched by the given criteria from the media
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the statement can count all records from the
current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

Both, the strings for ":joins" and for ":cond" are the same as for
the "search" SQL statement.

Contrary to the "search" statement, it doesn't return any records
but instead the number of records that have been found. As counting
thousands of records can be a long running task, the maximum number
of counted records is limited for performance reasons.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/lists/type/insert/ansi
* mshop/media/manager/lists/type/update/ansi
* mshop/media/manager/lists/type/newid/ansi
* mshop/media/manager/lists/type/delete/ansi
* mshop/media/manager/lists/type/search/ansi

## type/count/mysql

Counts the number of records matched by the given criteria in the database

```
mshop/media/manager/lists/type/count/mysql = 
 SELECT COUNT(*) AS "count"
 FROM(
 	SELECT mmedlity."id"
 	FROM "mshop_media_list_type" mmedlity
 	:joins
 	WHERE :cond
 	ORDER BY mmedlity."id"
 	LIMIT 10000 OFFSET 0
 ) AS list
```

* Default: 
 SELECT COUNT(*) AS "count"
 FROM(
 	SELECT mmedlity."id"
 	FROM "mshop_media_list_type" mmedlity
 	:joins
 	WHERE :cond
 	ORDER BY mmedlity."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list


See also:

* mshop/media/manager/lists/type/count/ansi

## type/decorators/excludes

Excludes decorators added by the "common" option from the media list type manager

```
mshop/media/manager/lists/type/decorators/excludes = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to remove a decorator added via
"mshop/common/manager/decorators/default" before they are wrapped
around the media list type manager.

```
 mshop/media/manager/lists/type/decorators/excludes = array( 'decorator1' )
```

This would remove the decorator named "decorator1" from the list of
common decorators ("\Aimeos\MShop\Common\Manager\Decorator\*") added via
"mshop/common/manager/decorators/default" for the media list type manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/lists/type/decorators/global
* mshop/media/manager/lists/type/decorators/local

## type/decorators/global

Adds a list of globally available decorators only to the media list type manager

```
mshop/media/manager/lists/type/decorators/global = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap global decorators
("\Aimeos\MShop\Common\Manager\Decorator\*") around the media list type
manager.

```
 mshop/media/manager/lists/type/decorators/global = array( 'decorator1' )
```

This would add the decorator named "decorator1" defined by
"\Aimeos\MShop\Common\Manager\Decorator\Decorator1" only to the media
list type manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/lists/type/decorators/excludes
* mshop/media/manager/lists/type/decorators/local

## type/decorators/local

Adds a list of local decorators only to the media list type manager

```
mshop/media/manager/lists/type/decorators/local = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap local decorators
("\Aimeos\MShop\Media\Manager\Lists\Type\Decorator\*") around the media
list type manager.

```
 mshop/media/manager/lists/type/decorators/local = array( 'decorator2' )
```

This would add the decorator named "decorator2" defined by
"\Aimeos\MShop\Media\Manager\Lists\Type\Decorator\Decorator2" only to the
media list type manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/lists/type/decorators/excludes
* mshop/media/manager/lists/type/decorators/global

## type/delete/ansi

Deletes the items matched by the given IDs from the database

```
mshop/media/manager/lists/type/delete/ansi = 
 DELETE FROM "mshop_media_list_type"
 WHERE :cond AND "siteid" LIKE ?
```

* Default: mshop/media/manager/lists/type/delete
* Type: string - SQL statement for deleting items
* Since: 2014.03

Removes the records specified by the given IDs from the media database.
The records must be from the site that is configured via the
context item.

The ":cond" placeholder is replaced by the name of the ID column and
the given ID or list of IDs while the site ID is bound to the question
mark.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/lists/type/insert/ansi
* mshop/media/manager/lists/type/update/ansi
* mshop/media/manager/lists/type/newid/ansi
* mshop/media/manager/lists/type/search/ansi
* mshop/media/manager/lists/type/count/ansi

## type/delete/mysql

Deletes the items matched by the given IDs from the database

```
mshop/media/manager/lists/type/delete/mysql = 
 DELETE FROM "mshop_media_list_type"
 WHERE :cond AND "siteid" LIKE ?
```

* Default: 
 DELETE FROM "mshop_media_list_type"
 WHERE :cond AND "siteid" LIKE ?


See also:

* mshop/media/manager/lists/type/delete/ansi

## type/insert/ansi

Inserts a new media list type record into the database table

```
mshop/media/manager/lists/type/insert/ansi = 
 INSERT INTO "mshop_media_list_type" ( :names
 	"code", "domain", "label", "pos", "status",
 	"mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?
 )
```

* Default: mshop/media/manager/lists/type/insert
* Type: string - SQL statement for inserting records
* Since: 2014.03

Items with no ID yet (i.e. the ID is NULL) will be created in
the database and the newly created ID retrieved afterwards
using the "newid" SQL statement.

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the media list type item to the statement before they are
sent to the database server. The number of question marks must
be the same as the number of columns listed in the INSERT
statement. The order of the columns must correspond to the
order in the save() method, so the correct values are
bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/lists/type/update/ansi
* mshop/media/manager/lists/type/newid/ansi
* mshop/media/manager/lists/type/delete/ansi
* mshop/media/manager/lists/type/search/ansi
* mshop/media/manager/lists/type/count/ansi

## type/insert/mysql

Inserts a new media list type record into the database table

```
mshop/media/manager/lists/type/insert/mysql = 
 INSERT INTO "mshop_media_list_type" ( :names
 	"code", "domain", "label", "pos", "status",
 	"mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?
 )
```

* Default: 
 INSERT INTO "mshop_media_list_type" ( :names
 	"code", "domain", "label", "pos", "status",
 	"mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?
 )


See also:

* mshop/media/manager/lists/type/insert/ansi

## type/name

Class name of the used media list type manager implementation

```
mshop/media/manager/lists/type/name = Standard
```

* Default: Standard
* Type: string - Last part of the class name
* Since: 2014.03

Each default media list type manager can be replaced by an alternative imlementation.
To use this implementation, you have to set the last part of the class
name as configuration value so the manager factory knows which class it
has to instantiate.

For example, if the name of the default class is

```
 \Aimeos\MShop\Media\Manager\Lists\Type\Standard
```

and you want to replace it with your own version named

```
 \Aimeos\MShop\Media\Manager\Lists\Type\Mytype
```

then you have to set the this configuration option:

```
 mshop/media/manager/lists/type/name = Mytype
```

The value is the last part of your own class name and it's case sensitive,
so take care that the configuration value is exactly named like the last
part of the class name.

The allowed characters of the class name are A-Z, a-z and 0-9. No other
characters are possible! You should always start the last part of the class
name with an upper case character and continue only with lower case characters
or numbers. Avoid chamel case names like "MyType"!


## type/newid/ansi

Retrieves the ID generated by the database when inserting a new record

```
mshop/media/manager/lists/type/newid/ansi = mshop/media/manager/lists/type/newid
```

* Default: mshop/media/manager/lists/type/newid
* Type: string - SQL statement for retrieving the last inserted record ID
* Since: 2014.03

As soon as a new record is inserted into the database table,
the database server generates a new and unique identifier for
that record. This ID can be used for retrieving, updating and
deleting that specific record from the table again.

For MySQL:
```
 SELECT LAST_INSERT_ID()
For PostgreSQL:
 SELECT currval('seq_mmedlity_id')
For SQL Server:
 SELECT SCOPE_IDENTITY()
For Oracle:
 SELECT "seq_mmedlity_id".CURRVAL FROM DUAL
```

There's no way to retrive the new ID by a SQL statements that
fits for most database servers as they implement their own
specific way.

See also:

* mshop/media/manager/lists/type/insert/ansi
* mshop/media/manager/lists/type/update/ansi
* mshop/media/manager/lists/type/delete/ansi
* mshop/media/manager/lists/type/search/ansi
* mshop/media/manager/lists/type/count/ansi

## type/newid/mysql

Retrieves the ID generated by the database when inserting a new record

```
mshop/media/manager/lists/type/newid/mysql = SELECT LAST_INSERT_ID()
```

* Default: mshop/media/manager/lists/type/newid

See also:

* mshop/media/manager/lists/type/newid/ansi

## type/search/ansi

Retrieves the records matched by the given criteria in the database

```
mshop/media/manager/lists/type/search/ansi = 
 SELECT :columns
 	mmedlity."id" AS "media.lists.type.id", mmedlity."siteid" AS "media.lists.type.siteid",
 	mmedlity."code" AS "media.lists.type.code", mmedlity."domain" AS "media.lists.type.domain",
 	mmedlity."label" AS "media.lists.type.label", mmedlity."status" AS "media.lists.type.status",
 	mmedlity."mtime" AS "media.lists.type.mtime", mmedlity."editor" AS "media.lists.type.editor",
 	mmedlity."ctime" AS "media.lists.type.ctime", mmedlity."pos" AS "media.lists.type.position"
 FROM "mshop_media_list_type" mmedlity
 :joins
 WHERE :cond
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY
```

* Default: mshop/media/manager/lists/type/search
* Type: string - SQL statement for searching items
* Since: 2014.03

Fetches the records matched by the given criteria from the media
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the SELECT statement can retrieve all records
from the current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

If the records that are retrieved should be ordered by one or more
columns, the generated string of column / sort direction pairs
replaces the ":order" placeholder. In case no ordering is required,
the complete ORDER BY part including the "/*-orderby*/.../*orderby-*/"
markers is removed to speed up retrieving the records. Columns of
sub-managers can also be used for ordering the result set but then
no index can be used.

The number of returned records can be limited and can start at any
number between the begining and the end of the result set. For that
the ":size" and ":start" placeholders are replaced by the
corresponding values from the criteria object. The default values
are 0 for the start and 100 for the size value.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/lists/type/insert/ansi
* mshop/media/manager/lists/type/update/ansi
* mshop/media/manager/lists/type/newid/ansi
* mshop/media/manager/lists/type/delete/ansi
* mshop/media/manager/lists/type/count/ansi

## type/search/mysql

Retrieves the records matched by the given criteria in the database

```
mshop/media/manager/lists/type/search/mysql = 
 SELECT :columns
 	mmedlity."id" AS "media.lists.type.id", mmedlity."siteid" AS "media.lists.type.siteid",
 	mmedlity."code" AS "media.lists.type.code", mmedlity."domain" AS "media.lists.type.domain",
 	mmedlity."label" AS "media.lists.type.label", mmedlity."status" AS "media.lists.type.status",
 	mmedlity."mtime" AS "media.lists.type.mtime", mmedlity."editor" AS "media.lists.type.editor",
 	mmedlity."ctime" AS "media.lists.type.ctime", mmedlity."pos" AS "media.lists.type.position"
 FROM "mshop_media_list_type" mmedlity
 :joins
 WHERE :cond
 ORDER BY :order
 LIMIT :size OFFSET :start
```

* Default: 
 SELECT :columns
 	mmedlity."id" AS "media.lists.type.id", mmedlity."siteid" AS "media.lists.type.siteid",
 	mmedlity."code" AS "media.lists.type.code", mmedlity."domain" AS "media.lists.type.domain",
 	mmedlity."label" AS "media.lists.type.label", mmedlity."status" AS "media.lists.type.status",
 	mmedlity."mtime" AS "media.lists.type.mtime", mmedlity."editor" AS "media.lists.type.editor",
 	mmedlity."ctime" AS "media.lists.type.ctime", mmedlity."pos" AS "media.lists.type.position"
 FROM "mshop_media_list_type" mmedlity
 :joins
 WHERE :cond
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY


See also:

* mshop/media/manager/lists/type/search/ansi

## type/submanagers

List of manager names that can be instantiated by the media list type manager

```
mshop/media/manager/lists/type/submanagers = Array
(
)
```

* Default: Array
(
)

* Type: array - List of sub-manager names
* Since: 2014.03

Managers provide a generic interface to the underlying storage.
Each manager has or can have sub-managers caring about particular
aspects. Each of these sub-managers can be instantiated by its
parent manager using the getSubManager() method.

The search keys from sub-managers can be normally used in the
manager as well. It allows you to search for items of the manager
using the search keys of the sub-managers to further limit the
retrieved list of items.


## type/update/ansi

Updates an existing media list type record in the database

```
mshop/media/manager/lists/type/update/ansi = 
 UPDATE "mshop_media_list_type"
 SET :names
 	"code" = ?, "domain" = ?, "label" = ?, "pos" = ?,
 	"status" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?
```

* Default: mshop/media/manager/lists/type/update
* Type: string - SQL statement for updating records
* Since: 2014.03

Items which already have an ID (i.e. the ID is not NULL) will
be updated in the database.

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the media list type item to the statement before they are
sent to the database server. The order of the columns must
correspond to the order in the save() method, so the
correct values are bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/lists/type/insert/ansi
* mshop/media/manager/lists/type/newid/ansi
* mshop/media/manager/lists/type/delete/ansi
* mshop/media/manager/lists/type/search/ansi
* mshop/media/manager/lists/type/count/ansi

## type/update/mysql

Updates an existing media list type record in the database

```
mshop/media/manager/lists/type/update/mysql = 
 UPDATE "mshop_media_list_type"
 SET :names
 	"code" = ?, "domain" = ?, "label" = ?, "pos" = ?,
 	"status" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?
```

* Default: 
 UPDATE "mshop_media_list_type"
 SET :names
 	"code" = ?, "domain" = ?, "label" = ?, "pos" = ?,
 	"status" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?


See also:

* mshop/media/manager/lists/type/update/ansi

## update/ansi

Updates an existing media list record in the database

```
mshop/media/manager/lists/update/ansi = 
 UPDATE "mshop_media_list"
 SET :names
 	"parentid"=?, "key" = ?, "type" = ?, "domain" = ?, "refid" = ?, "start" = ?,
 	"end" = ?, "config" = ?, "pos" = ?, "status" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?
```

* Default: mshop/media/manager/lists/update
* Type: string - SQL statement for updating records
* Since: 2014.03

Items which already have an ID (i.e. the ID is not NULL) will
be updated in the database.

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the media list item to the statement before they are
sent to the database server. The order of the columns must
correspond to the order in the save() method, so the
correct values are bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/lists/insert/ansi
* mshop/media/manager/lists/newid/ansi
* mshop/media/manager/lists/delete/ansi
* mshop/media/manager/lists/search/ansi
* mshop/media/manager/lists/count/ansi
* mshop/media/manager/lists/aggregate/ansi

## update/mysql

Updates an existing media list record in the database

```
mshop/media/manager/lists/update/mysql = 
 UPDATE "mshop_media_list"
 SET :names
 	"parentid"=?, "key" = ?, "type" = ?, "domain" = ?, "refid" = ?, "start" = ?,
 	"end" = ?, "config" = ?, "pos" = ?, "status" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?
```

* Default: 
 UPDATE "mshop_media_list"
 SET :names
 	"parentid"=?, "key" = ?, "type" = ?, "domain" = ?, "refid" = ?, "start" = ?,
 	"end" = ?, "config" = ?, "pos" = ?, "status" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?


See also:

* mshop/media/manager/lists/update/ansi

# name

Class name of the used media manager implementation

```
mshop/media/manager/name = Standard
```

* Default: Standard
* Type: string - Last part of the class name
* Since: 2014.03

Each default manager can be replace by an alternative imlementation.
To use this implementation, you have to set the last part of the class
name as configuration value so the manager factory knows which class it
has to instantiate.

For example, if the name of the default class is

```
 \Aimeos\MShop\Media\Manager\Standard
```

and you want to replace it with your own version named

```
 \Aimeos\MShop\Media\Manager\Mymanager
```

then you have to set the this configuration option:

```
 mshop/media/manager/name = Mymanager
```

The value is the last part of your own class name and it's case sensitive,
so take care that the configuration value is exactly named like the last
part of the class name.

The allowed characters of the class name are A-Z, a-z and 0-9. No other
characters are possible! You should always start the last part of the class
name with an upper case character and continue only with lower case characters
or numbers. Avoid chamel case names like "MyManager"!


# newid
## ansi

Retrieves the ID generated by the database when inserting a new record

```
mshop/media/manager/newid/ansi = mshop/media/manager/newid
```

* Default: mshop/media/manager/newid
* Type: string - SQL statement for retrieving the last inserted record ID
* Since: 2014.03

As soon as a new record is inserted into the database table,
the database server generates a new and unique identifier for
that record. This ID can be used for retrieving, updating and
deleting that specific record from the table again.

For MySQL:
```
 SELECT LAST_INSERT_ID()
For PostgreSQL:
 SELECT currval('seq_mmed_id')
For SQL Server:
 SELECT SCOPE_IDENTITY()
For Oracle:
 SELECT "seq_mmed_id".CURRVAL FROM DUAL
```

There's no way to retrive the new ID by a SQL statements that
fits for most database servers as they implement their own
specific way.

See also:

* mshop/media/manager/insert/ansi
* mshop/media/manager/update/ansi
* mshop/media/manager/delete/ansi
* mshop/media/manager/search/ansi
* mshop/media/manager/count/ansi

## mysql

Retrieves the ID generated by the database when inserting a new record

```
mshop/media/manager/newid/mysql = SELECT LAST_INSERT_ID()
```

* Default: mshop/media/manager/newid

See also:

* mshop/media/manager/newid/ansi

# property
## count/ansi

Counts the number of records matched by the given criteria in the database

```
mshop/media/manager/property/count/ansi = 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mmedpr."id"
 	FROM "mshop_media_property" mmedpr
 	:joins
 	WHERE :cond
 	ORDER BY mmedpr."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list
```

* Default: mshop/media/manager/property/count
* Type: string - SQL statement for counting items
* Since: 2018.01

Counts all records matched by the given criteria from the media
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the statement can count all records from the
current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

Both, the strings for ":joins" and for ":cond" are the same as for
the "search" SQL statement.

Contrary to the "search" statement, it doesn't return any records
but instead the number of records that have been found. As counting
thousands of records can be a long running task, the maximum number
of counted records is limited for performance reasons.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/property/insert/ansi
* mshop/media/manager/property/update/ansi
* mshop/media/manager/property/newid/ansi
* mshop/media/manager/property/delete/ansi
* mshop/media/manager/property/search/ansi

## count/mysql

Counts the number of records matched by the given criteria in the database

```
mshop/media/manager/property/count/mysql = 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mmedpr."id"
 	FROM "mshop_media_property" mmedpr
 	:joins
 	WHERE :cond
 	ORDER BY mmedpr."id"
 	LIMIT 10000 OFFSET 0
 ) AS list
```

* Default: 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mmedpr."id"
 	FROM "mshop_media_property" mmedpr
 	:joins
 	WHERE :cond
 	ORDER BY mmedpr."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list


See also:

* mshop/media/manager/property/count/ansi

## decorators/excludes

Excludes decorators added by the "common" option from the media property manager

```
mshop/media/manager/property/decorators/excludes = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2018.01

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to remove a decorator added via
"mshop/common/manager/decorators/default" before they are wrapped
around the media property manager.

```
 mshop/media/manager/property/decorators/excludes = array( 'decorator1' )
```

This would remove the decorator named "decorator1" from the list of
common decorators ("\Aimeos\MShop\Common\Manager\Decorator\*") added via
"mshop/common/manager/decorators/default" for the media property manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/property/decorators/global
* mshop/media/manager/property/decorators/local

## decorators/global

Adds a list of globally available decorators only to the media property manager

```
mshop/media/manager/property/decorators/global = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2018.01

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap global decorators
("\Aimeos\MShop\Common\Manager\Decorator\*") around the media property
manager.

```
 mshop/media/manager/property/decorators/global = array( 'decorator1' )
```

This would add the decorator named "decorator1" defined by
"\Aimeos\MShop\Common\Manager\Decorator\Decorator1" only to the media
property manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/property/decorators/excludes
* mshop/media/manager/property/decorators/local

## decorators/local

Adds a list of local decorators only to the media property manager

```
mshop/media/manager/property/decorators/local = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2018.01

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap local decorators
("\Aimeos\MShop\Media\Manager\Property\Decorator\*") around the media
property manager.

```
 mshop/media/manager/property/decorators/local = array( 'decorator2' )
```

This would add the decorator named "decorator2" defined by
"\Aimeos\MShop\Media\Manager\Property\Decorator\Decorator2" only to the
media property manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/property/decorators/excludes
* mshop/media/manager/property/decorators/global

## delete/ansi

Deletes the items matched by the given IDs from the database

```
mshop/media/manager/property/delete/ansi = 
 DELETE FROM "mshop_media_property"
 WHERE :cond AND "siteid" LIKE ?
```

* Default: mshop/media/manager/property/delete
* Type: string - SQL statement for deleting items
* Since: 2018.01

Removes the records specified by the given IDs from the media database.
The records must be from the site that is configured via the
context item.

The ":cond" placeholder is replaced by the name of the ID column and
the given ID or list of IDs while the site ID is bound to the question
mark.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/property/insert/ansi
* mshop/media/manager/property/update/ansi
* mshop/media/manager/property/newid/ansi
* mshop/media/manager/property/search/ansi
* mshop/media/manager/property/count/ansi

## delete/mysql

Deletes the items matched by the given IDs from the database

```
mshop/media/manager/property/delete/mysql = 
 DELETE FROM "mshop_media_property"
 WHERE :cond AND "siteid" LIKE ?
```

* Default: 
 DELETE FROM "mshop_media_property"
 WHERE :cond AND "siteid" LIKE ?


See also:

* mshop/media/manager/property/delete/ansi

## insert/ansi

Inserts a new media property record into the database table

```
mshop/media/manager/property/insert/ansi = 
 INSERT INTO "mshop_media_property" ( :names
 	"parentid", "key", "type", "langid", "value",
 	"mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?
 )
```

* Default: mshop/media/manager/property/insert
* Type: string - SQL statement for inserting records
* Since: 2018.01

Items with no ID yet (i.e. the ID is NULL) will be created in
the database and the newly created ID retrieved afterwards
using the "newid" SQL statement.

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the media property item to the statement before they are
sent to the database server. The number of question marks must
be the same as the number of columns listed in the INSERT
statement. The order of the columns must correspond to the
order in the save() method, so the correct values are
bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/property/update/ansi
* mshop/media/manager/property/newid/ansi
* mshop/media/manager/property/delete/ansi
* mshop/media/manager/property/search/ansi
* mshop/media/manager/property/count/ansi

## insert/mysql

Inserts a new media property record into the database table

```
mshop/media/manager/property/insert/mysql = 
 INSERT INTO "mshop_media_property" ( :names
 	"parentid", "key", "type", "langid", "value",
 	"mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?
 )
```

* Default: 
 INSERT INTO "mshop_media_property" ( :names
 	"parentid", "key", "type", "langid", "value",
 	"mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?
 )


See also:

* mshop/media/manager/property/insert/ansi

## name

Class name of the used media property manager implementation

```
mshop/media/manager/property/name = Standard
```

* Default: Standard
* Type: string - Last part of the class name
* Since: 2018.01

Each default media property manager can be replaced by an alternative imlementation.
To use this implementation, you have to set the last part of the class
name as configuration value so the manager factory knows which class it
has to instantiate.

For example, if the name of the default class is

```
 \Aimeos\MShop\Media\Manager\Property\Standard
```

and you want to replace it with your own version named

```
 \Aimeos\MShop\Media\Manager\Property\Myproperty
```

then you have to set the this configuration option:

```
 mshop/media/manager/property/name = Myproperty
```

The value is the last part of your own class name and it's case sensitive,
so take care that the configuration value is exactly named like the last
part of the class name.

The allowed characters of the class name are A-Z, a-z and 0-9. No other
characters are possible! You should always start the last part of the class
name with an upper case character and continue only with lower case characters
or numbers. Avoid chamel case names like "MyProperty"!


## newid/ansi

Retrieves the ID generated by the database when inserting a new record

```
mshop/media/manager/property/newid/ansi = mshop/media/manager/property/newid
```

* Default: mshop/media/manager/property/newid
* Type: string - SQL statement for retrieving the last inserted record ID
* Since: 2018.01

As soon as a new record is inserted into the database table,
the database server generates a new and unique identifier for
that record. This ID can be used for retrieving, updating and
deleting that specific record from the table again.

For MySQL:
```
 SELECT LAST_INSERT_ID()
For PostgreSQL:
 SELECT currval('seq_mmedpr_id')
For SQL Server:
 SELECT SCOPE_IDENTITY()
For Oracle:
 SELECT "seq_mmedpr_id".CURRVAL FROM DUAL
```

There's no way to retrive the new ID by a SQL statements that
fits for most database servers as they implement their own
specific way.

See also:

* mshop/media/manager/property/insert/ansi
* mshop/media/manager/property/update/ansi
* mshop/media/manager/property/delete/ansi
* mshop/media/manager/property/search/ansi
* mshop/media/manager/property/count/ansi

## newid/mysql

Retrieves the ID generated by the database when inserting a new record

```
mshop/media/manager/property/newid/mysql = SELECT LAST_INSERT_ID()
```

* Default: mshop/media/manager/property/newid

See also:

* mshop/media/manager/property/newid/ansi

## search/ansi

Retrieves the records matched by the given criteria in the database

```
mshop/media/manager/property/search/ansi = 
 SELECT :columns
 	mmedpr."id" AS "media.property.id", mmedpr."parentid" AS "media.property.parentid",
 	mmedpr."siteid" AS "media.property.siteid", mmedpr."type" AS "media.property.type",
 	mmedpr."langid" AS "media.property.languageid", mmedpr."value" AS "media.property.value",
 	mmedpr."mtime" AS "media.property.mtime", mmedpr."editor" AS "media.property.editor",
 	mmedpr."ctime" AS "media.property.ctime"
 FROM "mshop_media_property" mmedpr
 :joins
 WHERE :cond
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY
```

* Default: mshop/media/manager/property/search
* Type: string - SQL statement for searching items
* Since: 2018.01

Fetches the records matched by the given criteria from the media
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the SELECT statement can retrieve all records
from the current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

If the records that are retrieved should be ordered by one or more
columns, the generated string of column / sort direction pairs
replaces the ":order" placeholder. In case no ordering is required,
the complete ORDER BY part including the "/*-orderby*/.../*orderby-*/"
markers is removed to speed up retrieving the records. Columns of
sub-managers can also be used for ordering the result set but then
no index can be used.

The number of returned records can be limited and can start at any
number between the begining and the end of the result set. For that
the ":size" and ":start" placeholders are replaced by the
corresponding values from the criteria object. The default values
are 0 for the start and 100 for the size value.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/property/insert/ansi
* mshop/media/manager/property/update/ansi
* mshop/media/manager/property/newid/ansi
* mshop/media/manager/property/delete/ansi
* mshop/media/manager/property/count/ansi

## search/mysql

Retrieves the records matched by the given criteria in the database

```
mshop/media/manager/property/search/mysql = 
 SELECT :columns
 	mmedpr."id" AS "media.property.id", mmedpr."parentid" AS "media.property.parentid",
 	mmedpr."siteid" AS "media.property.siteid", mmedpr."type" AS "media.property.type",
 	mmedpr."langid" AS "media.property.languageid", mmedpr."value" AS "media.property.value",
 	mmedpr."mtime" AS "media.property.mtime", mmedpr."editor" AS "media.property.editor",
 	mmedpr."ctime" AS "media.property.ctime"
 FROM "mshop_media_property" mmedpr
 :joins
 WHERE :cond
 ORDER BY :order
 LIMIT :size OFFSET :start
```

* Default: 
 SELECT :columns
 	mmedpr."id" AS "media.property.id", mmedpr."parentid" AS "media.property.parentid",
 	mmedpr."siteid" AS "media.property.siteid", mmedpr."type" AS "media.property.type",
 	mmedpr."langid" AS "media.property.languageid", mmedpr."value" AS "media.property.value",
 	mmedpr."mtime" AS "media.property.mtime", mmedpr."editor" AS "media.property.editor",
 	mmedpr."ctime" AS "media.property.ctime"
 FROM "mshop_media_property" mmedpr
 :joins
 WHERE :cond
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY


See also:

* mshop/media/manager/property/search/ansi

## submanagers

List of manager names that can be instantiated by the media property manager

```
mshop/media/manager/property/submanagers = Array
(
)
```

* Default: Array
(
)

* Type: array - List of sub-manager names
* Since: 2018.01

Managers provide a generic interface to the underlying storage.
Each manager has or can have sub-managers caring about particular
aspects. Each of these sub-managers can be instantiated by its
parent manager using the getSubManager() method.

The search keys from sub-managers can be normally used in the
manager as well. It allows you to search for items of the manager
using the search keys of the sub-managers to further limit the
retrieved list of items.


## type/count/ansi

Counts the number of records matched by the given criteria in the database

```
mshop/media/manager/property/type/count/ansi = 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mmedprty."id"
 	FROM "mshop_media_property_type" mmedprty
 	:joins
 	WHERE :cond
 	ORDER BY mmedprty."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list
```

* Default: mshop/media/manager/property/type/count
* Type: string - SQL statement for counting items
* Since: 2018.01

Counts all records matched by the given criteria from the media
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the statement can count all records from the
current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

Both, the strings for ":joins" and for ":cond" are the same as for
the "search" SQL statement.

Contrary to the "search" statement, it doesn't return any records
but instead the number of records that have been found. As counting
thousands of records can be a long running task, the maximum number
of counted records is limited for performance reasons.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/property/type/insert/ansi
* mshop/media/manager/property/type/update/ansi
* mshop/media/manager/property/type/newid/ansi
* mshop/media/manager/property/type/delete/ansi
* mshop/media/manager/property/type/search/ansi

## type/count/mysql

Counts the number of records matched by the given criteria in the database

```
mshop/media/manager/property/type/count/mysql = 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mmedprty."id"
 	FROM "mshop_media_property_type" mmedprty
 	:joins
 	WHERE :cond
 	ORDER BY mmedprty."id"
 	LIMIT 10000 OFFSET 0
 ) AS list
```

* Default: 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mmedprty."id"
 	FROM "mshop_media_property_type" mmedprty
 	:joins
 	WHERE :cond
 	ORDER BY mmedprty."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list


See also:

* mshop/media/manager/property/type/count/ansi

## type/decorators/excludes

Excludes decorators added by the "common" option from the media property type manager

```
mshop/media/manager/property/type/decorators/excludes = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2018.01

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to remove a decorator added via
"mshop/common/manager/decorators/default" before they are wrapped
around the media property type manager.

```
 mshop/media/manager/property/type/decorators/excludes = array( 'decorator1' )
```

This would remove the decorator named "decorator1" from the list of
common decorators ("\Aimeos\MShop\Common\Manager\Decorator\*") added via
"mshop/common/manager/decorators/default" for the media property type manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/property/type/decorators/global
* mshop/media/manager/property/type/decorators/local

## type/decorators/global

Adds a list of globally available decorators only to the media property type manager

```
mshop/media/manager/property/type/decorators/global = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2018.01

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap global decorators
("\Aimeos\MShop\Common\Manager\Decorator\*") around the media property
type manager.

```
 mshop/media/manager/property/type/decorators/global = array( 'decorator1' )
```

This would add the decorator named "decorator1" defined by
"\Aimeos\MShop\Common\Manager\Decorator\Decorator1" only to the media
property type manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/property/type/decorators/excludes
* mshop/media/manager/property/type/decorators/local

## type/decorators/local

Adds a list of local decorators only to the media property type manager

```
mshop/media/manager/property/type/decorators/local = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2018.01

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap local decorators
("\Aimeos\MShop\Media\Manager\Property\Type\Decorator\*") around the
media property type manager.

```
 mshop/media/manager/property/type/decorators/local = array( 'decorator2' )
```

This would add the decorator named "decorator2" defined by
"\Aimeos\MShop\Media\Manager\Property\Type\Decorator\Decorator2" only
to the media property type manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/property/type/decorators/excludes
* mshop/media/manager/property/type/decorators/global

## type/delete/ansi

Deletes the items matched by the given IDs from the database

```
mshop/media/manager/property/type/delete/ansi = 
 DELETE FROM "mshop_media_property_type"
 WHERE :cond AND "siteid" LIKE ?
```

* Default: mshop/media/manager/property/type/delete
* Type: string - SQL statement for deleting items
* Since: 2018.01

Removes the records specified by the given IDs from the media database.
The records must be from the site that is configured via the
context item.

The ":cond" placeholder is replaced by the name of the ID column and
the given ID or list of IDs while the site ID is bound to the question
mark.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/property/type/insert/ansi
* mshop/media/manager/property/type/update/ansi
* mshop/media/manager/property/type/newid/ansi
* mshop/media/manager/property/type/search/ansi
* mshop/media/manager/property/type/count/ansi

## type/delete/mysql

Deletes the items matched by the given IDs from the database

```
mshop/media/manager/property/type/delete/mysql = 
 DELETE FROM "mshop_media_property_type"
 WHERE :cond AND "siteid" LIKE ?
```

* Default: 
 DELETE FROM "mshop_media_property_type"
 WHERE :cond AND "siteid" LIKE ?


See also:

* mshop/media/manager/property/type/delete/ansi

## type/insert/ansi

Inserts a new media property type record into the database table

```
mshop/media/manager/property/type/insert/ansi = 
 INSERT INTO "mshop_media_property_type" ( :names
 	"code", "domain", "label", "pos", "status",
 	"mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?
 )
```

* Default: mshop/media/manager/property/type/insert
* Type: string - SQL statement for inserting records
* Since: 2018.01

Items with no ID yet (i.e. the ID is NULL) will be created in
the database and the newly created ID retrieved afterwards
using the "newid" SQL statement.

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the media type item to the statement before they are
sent to the database server. The number of question marks must
be the same as the number of columns listed in the INSERT
statement. The order of the columns must correspond to the
order in the save() method, so the correct values are
bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/property/type/update/ansi
* mshop/media/manager/property/type/newid/ansi
* mshop/media/manager/property/type/delete/ansi
* mshop/media/manager/property/type/search/ansi
* mshop/media/manager/property/type/count/ansi

## type/insert/mysql

Inserts a new media property type record into the database table

```
mshop/media/manager/property/type/insert/mysql = 
 INSERT INTO "mshop_media_property_type" ( :names
 	"code", "domain", "label", "pos", "status",
 	"mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?
 )
```

* Default: 
 INSERT INTO "mshop_media_property_type" ( :names
 	"code", "domain", "label", "pos", "status",
 	"mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?
 )


See also:

* mshop/media/manager/property/type/insert/ansi

## type/name

Class name of the used media property type manager implementation

```
mshop/media/manager/property/type/name = Standard
```

* Default: Standard
* Type: string - Last part of the class name
* Since: 2018.01

Each default media property type manager can be replaced by an alternative imlementation.
To use this implementation, you have to set the last part of the class
name as configuration value so the manager factory knows which class it
has to instantiate.

For example, if the name of the default class is

```
 \Aimeos\MShop\Media\Manager\Lists\Type\Standard
```

and you want to replace it with your own version named

```
 \Aimeos\MShop\Media\Manager\Lists\Type\Mytype
```

then you have to set the this configuration option:

```
 mshop/media/manager/property/type/name = Mytype
```

The value is the last part of your own class name and it's case sensitive,
so take care that the configuration value is exactly named like the last
part of the class name.

The allowed characters of the class name are A-Z, a-z and 0-9. No other
characters are possible! You should always start the last part of the class
name with an upper case character and continue only with lower case characters
or numbers. Avoid chamel case names like "MyType"!


## type/newid/ansi

Retrieves the ID generated by the database when inserting a new record

```
mshop/media/manager/property/type/newid/ansi = mshop/media/manager/property/type/newid
```

* Default: mshop/media/manager/property/type/newid
* Type: string - SQL statement for retrieving the last inserted record ID
* Since: 2018.01

As soon as a new record is inserted into the database table,
the database server generates a new and unique identifier for
that record. This ID can be used for retrieving, updating and
deleting that specific record from the table again.

For MySQL:
```
 SELECT LAST_INSERT_ID()
For PostgreSQL:
 SELECT currval('seq_mmedprty_id')
For SQL Server:
 SELECT SCOPE_IDENTITY()
For Oracle:
 SELECT "seq_mmedprty_id".CURRVAL FROM DUAL
```

There's no way to retrive the new ID by a SQL statements that
fits for most database servers as they implement their own
specific way.

See also:

* mshop/media/manager/property/type/insert/ansi
* mshop/media/manager/property/type/update/ansi
* mshop/media/manager/property/type/delete/ansi
* mshop/media/manager/property/type/search/ansi
* mshop/media/manager/property/type/count/ansi

## type/newid/mysql

Retrieves the ID generated by the database when inserting a new record

```
mshop/media/manager/property/type/newid/mysql = SELECT LAST_INSERT_ID()
```

* Default: mshop/media/manager/property/type/newid

See also:

* mshop/media/manager/property/type/newid/ansi

## type/search/ansi

Retrieves the records matched by the given criteria in the database

```
mshop/media/manager/property/type/search/ansi = 
 SELECT :columns
 	mmedprty."id" AS "media.property.type.id", mmedprty."siteid" AS "media.property.type.siteid",
 	mmedprty."code" AS "media.property.type.code", mmedprty."domain" AS "media.property.type.domain",
 	mmedprty."label" AS "media.property.type.label", mmedprty."status" AS "media.property.type.status",
 	mmedprty."mtime" AS "media.property.type.mtime", mmedprty."editor" AS "media.property.type.editor",
 	mmedprty."ctime" AS "media.property.type.ctime", mmedprty."pos" AS "media.property.type.position"
 FROM "mshop_media_property_type" mmedprty
 :joins
 WHERE :cond
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY
```

* Default: mshop/media/manager/property/type/search
* Type: string - SQL statement for searching items
* Since: 2018.01

Fetches the records matched by the given criteria from the media
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the SELECT statement can retrieve all records
from the current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

If the records that are retrieved should be ordered by one or more
columns, the generated string of column / sort direction pairs
replaces the ":order" placeholder. In case no ordering is required,
the complete ORDER BY part including the "/*-orderby*/.../*orderby-*/"
markers is removed to speed up retrieving the records. Columns of
sub-managers can also be used for ordering the result set but then
no index can be used.

The number of returned records can be limited and can start at any
number between the begining and the end of the result set. For that
the ":size" and ":start" placeholders are replaced by the
corresponding values from the criteria object. The default values
are 0 for the start and 100 for the size value.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/property/type/insert/ansi
* mshop/media/manager/property/type/update/ansi
* mshop/media/manager/property/type/newid/ansi
* mshop/media/manager/property/type/delete/ansi
* mshop/media/manager/property/type/count/ansi

## type/search/mysql

Retrieves the records matched by the given criteria in the database

```
mshop/media/manager/property/type/search/mysql = 
 SELECT :columns
 	mmedprty."id" AS "media.property.type.id", mmedprty."siteid" AS "media.property.type.siteid",
 	mmedprty."code" AS "media.property.type.code", mmedprty."domain" AS "media.property.type.domain",
 	mmedprty."label" AS "media.property.type.label", mmedprty."status" AS "media.property.type.status",
 	mmedprty."mtime" AS "media.property.type.mtime", mmedprty."editor" AS "media.property.type.editor",
 	mmedprty."ctime" AS "media.property.type.ctime", mmedprty."pos" AS "media.property.type.position"
 FROM "mshop_media_property_type" mmedprty
 :joins
 WHERE :cond
 ORDER BY :order
 LIMIT :size OFFSET :start
```

* Default: 
 SELECT :columns
 	mmedprty."id" AS "media.property.type.id", mmedprty."siteid" AS "media.property.type.siteid",
 	mmedprty."code" AS "media.property.type.code", mmedprty."domain" AS "media.property.type.domain",
 	mmedprty."label" AS "media.property.type.label", mmedprty."status" AS "media.property.type.status",
 	mmedprty."mtime" AS "media.property.type.mtime", mmedprty."editor" AS "media.property.type.editor",
 	mmedprty."ctime" AS "media.property.type.ctime", mmedprty."pos" AS "media.property.type.position"
 FROM "mshop_media_property_type" mmedprty
 :joins
 WHERE :cond
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY


See also:

* mshop/media/manager/property/type/search/ansi

## type/submanagers

List of manager names that can be instantiated by the media property type manager

```
mshop/media/manager/property/type/submanagers = Array
(
)
```

* Default: Array
(
)

* Type: array - List of sub-manager names
* Since: 2018.01

Managers provide a generic interface to the underlying storage.
Each manager has or can have sub-managers caring about particular
aspects. Each of these sub-managers can be instantiated by its
parent manager using the getSubManager() method.

The search keys from sub-managers can be normally used in the
manager as well. It allows you to search for items of the manager
using the search keys of the sub-managers to further limit the
retrieved list of items.


## type/update/ansi

Updates an existing media property type record in the database

```
mshop/media/manager/property/type/update/ansi = 
 UPDATE "mshop_media_property_type"
 SET :names
 	"code" = ?, "domain" = ?, "label" = ?, "pos" = ?,
 	"status" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?
```

* Default: mshop/media/manager/property/type/update
* Type: string - SQL statement for updating records
* Since: 2018.01

Items which already have an ID (i.e. the ID is not NULL) will
be updated in the database.

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the media type item to the statement before they are
sent to the database server. The order of the columns must
correspond to the order in the save() method, so the
correct values are bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/property/type/insert/ansi
* mshop/media/manager/property/type/newid/ansi
* mshop/media/manager/property/type/delete/ansi
* mshop/media/manager/property/type/search/ansi
* mshop/media/manager/property/type/count/ansi

## type/update/mysql

Updates an existing media property type record in the database

```
mshop/media/manager/property/type/update/mysql = 
 UPDATE "mshop_media_property_type"
 SET :names
 	"code" = ?, "domain" = ?, "label" = ?, "pos" = ?,
 	"status" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?
```

* Default: 
 UPDATE "mshop_media_property_type"
 SET :names
 	"code" = ?, "domain" = ?, "label" = ?, "pos" = ?,
 	"status" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?


See also:

* mshop/media/manager/property/type/update/ansi

## update/ansi

Updates an existing media property record in the database

```
mshop/media/manager/property/update/ansi = 
 UPDATE "mshop_media_property"
 SET :names
 	"parentid" = ?, "key" = ?, "type" = ?, "langid" = ?,
 	"value" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?
```

* Default: mshop/media/manager/property/update
* Type: string - SQL statement for updating records
* Since: 2018.01

Items which already have an ID (i.e. the ID is not NULL) will
be updated in the database.

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the media property item to the statement before they are
sent to the database server. The order of the columns must
correspond to the order in the save() method, so the
correct values are bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/property/insert/ansi
* mshop/media/manager/property/newid/ansi
* mshop/media/manager/property/delete/ansi
* mshop/media/manager/property/search/ansi
* mshop/media/manager/property/count/ansi

## update/mysql

Updates an existing media property record in the database

```
mshop/media/manager/property/update/mysql = 
 UPDATE "mshop_media_property"
 SET :names
 	"parentid" = ?, "key" = ?, "type" = ?, "langid" = ?,
 	"value" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?
```

* Default: 
 UPDATE "mshop_media_property"
 SET :names
 	"parentid" = ?, "key" = ?, "type" = ?, "langid" = ?,
 	"value" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?


See also:

* mshop/media/manager/property/update/ansi

# search
## ansi

Retrieves the records matched by the given criteria in the database

```
mshop/media/manager/search/ansi = 
 SELECT :columns
 	mmed."id" AS "media.id", mmed."siteid" AS "media.siteid",
 	mmed."langid" AS "media.languageid", mmed."type" AS "media.type",
 	mmed."link" AS "media.url", mmed."label" AS "media.label",
 	mmed."status" AS "media.status", mmed."mimetype" AS "media.mimetype",
 	mmed."domain" AS "media.domain", mmed."preview" AS "media.previews",
 	mmed."fsname" AS "media.filesystem", mmed."mtime" AS "media.mtime",
 	mmed."ctime" AS "media.ctime", mmed."editor" AS "media.editor"
 FROM "mshop_media" mmed
 :joins
 WHERE :cond
 GROUP BY :columns :group
 	mmed."id", mmed."siteid", mmed."langid", mmed."type", mmed."link",
 	mmed."label", mmed."status", mmed."mimetype", mmed."domain", mmed."preview",
 	mmed."fsname", mmed."mtime", mmed."editor", mmed."ctime"
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY
```

* Default: mshop/media/manager/search
* Type: string - SQL statement for searching items
* Since: 2014.03

Fetches the records matched by the given criteria from the media
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the SELECT statement can retrieve all records
from the current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

If the records that are retrieved should be ordered by one or more
columns, the generated string of column / sort direction pairs
replaces the ":order" placeholder. In case no ordering is required,
the complete ORDER BY part including the "/*-orderby*/.../*orderby-*/"
markers is removed to speed up retrieving the records. Columns of
sub-managers can also be used for ordering the result set but then
no index can be used.

The number of returned records can be limited and can start at any
number between the begining and the end of the result set. For that
the ":size" and ":start" placeholders are replaced by the
corresponding values from the criteria object. The default values
are 0 for the start and 100 for the size value.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/insert/ansi
* mshop/media/manager/update/ansi
* mshop/media/manager/newid/ansi
* mshop/media/manager/delete/ansi
* mshop/media/manager/count/ansi

## mysql

Retrieves the records matched by the given criteria in the database

```
mshop/media/manager/search/mysql = 
 SELECT :columns
 	mmed."id" AS "media.id", mmed."siteid" AS "media.siteid",
 	mmed."langid" AS "media.languageid", mmed."type" AS "media.type",
 	mmed."link" AS "media.url", mmed."label" AS "media.label",
 	mmed."status" AS "media.status", mmed."mimetype" AS "media.mimetype",
 	mmed."domain" AS "media.domain", mmed."preview" AS "media.previews",
 	mmed."fsname" AS "media.filesystem", mmed."mtime" AS "media.mtime",
 	mmed."ctime" AS "media.ctime", mmed."editor" AS "media.editor"
 FROM "mshop_media" mmed
 :joins
 WHERE :cond
 GROUP BY :group mmed."id"
 ORDER BY :order
 LIMIT :size OFFSET :start
```

* Default: 
 SELECT :columns
 	mmed."id" AS "media.id", mmed."siteid" AS "media.siteid",
 	mmed."langid" AS "media.languageid", mmed."type" AS "media.type",
 	mmed."link" AS "media.url", mmed."label" AS "media.label",
 	mmed."status" AS "media.status", mmed."mimetype" AS "media.mimetype",
 	mmed."domain" AS "media.domain", mmed."preview" AS "media.previews",
 	mmed."fsname" AS "media.filesystem", mmed."mtime" AS "media.mtime",
 	mmed."ctime" AS "media.ctime", mmed."editor" AS "media.editor"
 FROM "mshop_media" mmed
 :joins
 WHERE :cond
 GROUP BY :columns :group
 	mmed."id", mmed."siteid", mmed."langid", mmed."type", mmed."link",
 	mmed."label", mmed."status", mmed."mimetype", mmed."domain", mmed."preview",
 	mmed."fsname", mmed."mtime", mmed."editor", mmed."ctime"
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY


See also:

* mshop/media/manager/search/ansi

# sitemode

Mode how items from levels below or above in the site tree are handled

```
mshop/media/manager/sitemode = 3
```

* Default: 3
* Type: int - Constant from Aimeos\MShop\Locale\Manager\Base class
* Since: 2018.01

By default, only items from the current site are fetched from the
storage. If the ai-sites extension is installed, you can create a
tree of sites. Then, this setting allows you to define for the
whole media domain if items from parent sites are inherited,
sites from child sites are aggregated or both.

Available constants for the site mode are:
* 0 = only items from the current site
* 1 = inherit items from parent sites
* 2 = aggregate items from child sites
* 3 = inherit and aggregate items at the same time

You also need to set the mode in the locale manager
(mshop/locale/manager/sitelevel) to one of the constants.
If you set it to the same value, it will work as described but you
can also use different modes. For example, if inheritance and
aggregation is configured the locale manager but only inheritance
in the domain manager because aggregating items makes no sense in
this domain, then items wil be only inherited. Thus, you have full
control over inheritance and aggregation in each domain.

See also:

* mshop/locale/manager/sitelevel

# submanagers

List of manager names that can be instantiated by the media manager

```
mshop/media/manager/submanagers = Array
(
)
```

* Default: Array
(
)

* Type: array - List of sub-manager names
* Since: 2014.03

Managers provide a generic interface to the underlying storage.
Each manager has or can have sub-managers caring about particular
aspects. Each of these sub-managers can be instantiated by its
parent manager using the getSubManager() method.

The search keys from sub-managers can be normally used in the
manager as well. It allows you to search for items of the manager
using the search keys of the sub-managers to further limit the
retrieved list of items.


# type
## count/ansi

Counts the number of records matched by the given criteria in the database

```
mshop/media/manager/type/count/ansi = 
 SELECT COUNT(*) AS "count"
 FROM(
 	SELECT mmedty."id"
 	FROM "mshop_media_type" mmedty
 	:joins
 	WHERE :cond
 	ORDER BY mmedty."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list
```

* Default: mshop/media/manager/type/count
* Type: string - SQL statement for counting items
* Since: 2014.03

Counts all records matched by the given criteria from the media
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the statement can count all records from the
current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

Both, the strings for ":joins" and for ":cond" are the same as for
the "search" SQL statement.

Contrary to the "search" statement, it doesn't return any records
but instead the number of records that have been found. As counting
thousands of records can be a long running task, the maximum number
of counted records is limited for performance reasons.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/type/insert/ansi
* mshop/media/manager/type/update/ansi
* mshop/media/manager/type/newid/ansi
* mshop/media/manager/type/delete/ansi
* mshop/media/manager/type/search/ansi

## count/mysql

Counts the number of records matched by the given criteria in the database

```
mshop/media/manager/type/count/mysql = 
 SELECT COUNT(*) AS "count"
 FROM(
 	SELECT mmedty."id"
 	FROM "mshop_media_type" mmedty
 	:joins
 	WHERE :cond
 	ORDER BY mmedty."id"
 	LIMIT 10000 OFFSET 0
 ) AS list
```

* Default: 
 SELECT COUNT(*) AS "count"
 FROM(
 	SELECT mmedty."id"
 	FROM "mshop_media_type" mmedty
 	:joins
 	WHERE :cond
 	ORDER BY mmedty."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list


See also:

* mshop/media/manager/type/count/ansi

## decorators/excludes

Excludes decorators added by the "common" option from the media type manager

```
mshop/media/manager/type/decorators/excludes = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to remove a decorator added via
"mshop/common/manager/decorators/default" before they are wrapped
around the media type manager.

```
 mshop/media/manager/type/decorators/excludes = array( 'decorator1' )
```

This would remove the decorator named "decorator1" from the list of
common decorators ("\Aimeos\MShop\Common\Manager\Decorator\*") added via
"mshop/common/manager/decorators/default" for the media type manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/type/decorators/global
* mshop/media/manager/type/decorators/local

## decorators/global

Adds a list of globally available decorators only to the media type manager

```
mshop/media/manager/type/decorators/global = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap global decorators
("\Aimeos\MShop\Media\Manager\Type\Decorator\*") around the media type
manager.

```
 mshop/media/manager/type/decorators/global = array( 'decorator1' )
```

This would add the decorator named "decorator1" defined by
"\Aimeos\MShop\Media\Manager\Type\Decorator\Decorator1" only to the media
type manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/type/decorators/excludes
* mshop/media/manager/type/decorators/local

## decorators/local

Adds a list of local decorators only to the media type manager

```
mshop/media/manager/type/decorators/local = Array
(
)
```

* Default: Array
(
)

* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap local decorators
("\Aimeos\MShop\Media\Manager\Type\Decorator\*") around the media type
manager.

```
 mshop/media/manager/type/decorators/local = array( 'decorator2' )
```

This would add the decorator named "decorator2" defined by
"\Aimeos\MShop\Media\Manager\Type\Decorator\Decorator2" only to the
media type manager.

See also:

* mshop/common/manager/decorators/default
* mshop/media/manager/type/decorators/excludes
* mshop/media/manager/type/decorators/global

## delete/ansi

Deletes the items matched by the given IDs from the database

```
mshop/media/manager/type/delete/ansi = 
 DELETE FROM "mshop_media_type"
 WHERE :cond AND "siteid" LIKE ?
```

* Default: mshop/media/manager/type/delete
* Type: string - SQL statement for deleting items
* Since: 2014.03

Removes the records specified by the given IDs from the media database.
The records must be from the site that is configured via the
context item.

The ":cond" placeholder is replaced by the name of the ID column and
the given ID or list of IDs while the site ID is bound to the question
mark.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/type/insert/ansi
* mshop/media/manager/type/update/ansi
* mshop/media/manager/type/newid/ansi
* mshop/media/manager/type/search/ansi
* mshop/media/manager/type/count/ansi

## delete/mysql

Deletes the items matched by the given IDs from the database

```
mshop/media/manager/type/delete/mysql = 
 DELETE FROM "mshop_media_type"
 WHERE :cond AND "siteid" LIKE ?
```

* Default: 
 DELETE FROM "mshop_media_type"
 WHERE :cond AND "siteid" LIKE ?


See also:

* mshop/media/manager/type/delete/ansi

## insert/ansi

Inserts a new media type record into the database table

```
mshop/media/manager/type/insert/ansi = 
 INSERT INTO "mshop_media_type" ( :names
 	"code", "domain", "label", "pos", "status",
 	"mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?
 )
```

* Default: mshop/media/manager/type/insert
* Type: string - SQL statement for inserting records
* Since: 2014.03

Items with no ID yet (i.e. the ID is NULL) will be created in
the database and the newly created ID retrieved afterwards
using the "newid" SQL statement.

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the media type item to the statement before they are
sent to the database server. The number of question marks must
be the same as the number of columns listed in the INSERT
statement. The order of the columns must correspond to the
order in the save() method, so the correct values are
bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/type/update/ansi
* mshop/media/manager/type/newid/ansi
* mshop/media/manager/type/delete/ansi
* mshop/media/manager/type/search/ansi
* mshop/media/manager/type/count/ansi

## insert/mysql

Inserts a new media type record into the database table

```
mshop/media/manager/type/insert/mysql = 
 INSERT INTO "mshop_media_type" ( :names
 	"code", "domain", "label", "pos", "status",
 	"mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?
 )
```

* Default: 
 INSERT INTO "mshop_media_type" ( :names
 	"code", "domain", "label", "pos", "status",
 	"mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?, ?
 )


See also:

* mshop/media/manager/type/insert/ansi

## name

Class name of the used media type manager implementation

```
mshop/media/manager/type/name = Standard
```

* Default: Standard
* Type: string - Last part of the class name
* Since: 2014.03

Each default media type manager can be replaced by an alternative imlementation.
To use this implementation, you have to set the last part of the class
name as configuration value so the manager factory knows which class it
has to instantiate.

For example, if the name of the default class is

```
 \Aimeos\MShop\Media\Manager\Type\Standard
```

and you want to replace it with your own version named

```
 \Aimeos\MShop\Media\Manager\Type\Mytype
```

then you have to set the this configuration option:

```
 mshop/media/manager/type/name = Mytype
```

The value is the last part of your own class name and it's case sensitive,
so take care that the configuration value is exactly named like the last
part of the class name.

The allowed characters of the class name are A-Z, a-z and 0-9. No other
characters are possible! You should always start the last part of the class
name with an upper case character and continue only with lower case characters
or numbers. Avoid chamel case names like "MyType"!


## newid/ansi

Retrieves the ID generated by the database when inserting a new record

```
mshop/media/manager/type/newid/ansi = mshop/media/manager/type/newid
```

* Default: mshop/media/manager/type/newid
* Type: string - SQL statement for retrieving the last inserted record ID
* Since: 2014.03

As soon as a new record is inserted into the database table,
the database server generates a new and unique identifier for
that record. This ID can be used for retrieving, updating and
deleting that specific record from the table again.

For MySQL:
```
 SELECT LAST_INSERT_ID()
For PostgreSQL:
 SELECT currval('seq_mmedty_id')
For SQL Server:
 SELECT SCOPE_IDENTITY()
For Oracle:
 SELECT "seq_mmedty_id".CURRVAL FROM DUAL
```

There's no way to retrive the new ID by a SQL statements that
fits for most database servers as they implement their own
specific way.

See also:

* mshop/media/manager/type/insert/ansi
* mshop/media/manager/type/update/ansi
* mshop/media/manager/type/delete/ansi
* mshop/media/manager/type/search/ansi
* mshop/media/manager/type/count/ansi

## newid/mysql

Retrieves the ID generated by the database when inserting a new record

```
mshop/media/manager/type/newid/mysql = SELECT LAST_INSERT_ID()
```

* Default: mshop/media/manager/type/newid

See also:

* mshop/media/manager/type/newid/ansi

## search/ansi

Retrieves the records matched by the given criteria in the database

```
mshop/media/manager/type/search/ansi = 
 SELECT :columns
 	mmedty."id" AS "media.type.id", mmedty."siteid" AS "media.type.siteid",
 	mmedty."code" AS "media.type.code", mmedty."domain" AS "media.type.domain",
 	mmedty."label" AS "media.type.label", mmedty."status" AS "media.type.status",
 	mmedty."mtime" AS "media.type.mtime", mmedty."editor" AS "media.type.editor",
 	mmedty."ctime" AS "media.type.ctime", mmedty."pos" AS "media.type.position"
 FROM "mshop_media_type" mmedty
 :joins
 WHERE :cond
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY
```

* Default: mshop/media/manager/type/search
* Type: string - SQL statement for searching items
* Since: 2014.03

Fetches the records matched by the given criteria from the media
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the SELECT statement can retrieve all records
from the current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

If the records that are retrieved should be ordered by one or more
columns, the generated string of column / sort direction pairs
replaces the ":order" placeholder. In case no ordering is required,
the complete ORDER BY part including the "/*-orderby*/.../*orderby-*/"
markers is removed to speed up retrieving the records. Columns of
sub-managers can also be used for ordering the result set but then
no index can be used.

The number of returned records can be limited and can start at any
number between the begining and the end of the result set. For that
the ":size" and ":start" placeholders are replaced by the
corresponding values from the criteria object. The default values
are 0 for the start and 100 for the size value.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/type/insert/ansi
* mshop/media/manager/type/update/ansi
* mshop/media/manager/type/newid/ansi
* mshop/media/manager/type/delete/ansi
* mshop/media/manager/type/count/ansi

## search/mysql

Retrieves the records matched by the given criteria in the database

```
mshop/media/manager/type/search/mysql = 
 SELECT :columns
 	mmedty."id" AS "media.type.id", mmedty."siteid" AS "media.type.siteid",
 	mmedty."code" AS "media.type.code", mmedty."domain" AS "media.type.domain",
 	mmedty."label" AS "media.type.label", mmedty."status" AS "media.type.status",
 	mmedty."mtime" AS "media.type.mtime", mmedty."editor" AS "media.type.editor",
 	mmedty."ctime" AS "media.type.ctime", mmedty."pos" AS "media.type.position"
 FROM "mshop_media_type" mmedty
 :joins
 WHERE :cond
 ORDER BY :order
 LIMIT :size OFFSET :start
```

* Default: 
 SELECT :columns
 	mmedty."id" AS "media.type.id", mmedty."siteid" AS "media.type.siteid",
 	mmedty."code" AS "media.type.code", mmedty."domain" AS "media.type.domain",
 	mmedty."label" AS "media.type.label", mmedty."status" AS "media.type.status",
 	mmedty."mtime" AS "media.type.mtime", mmedty."editor" AS "media.type.editor",
 	mmedty."ctime" AS "media.type.ctime", mmedty."pos" AS "media.type.position"
 FROM "mshop_media_type" mmedty
 :joins
 WHERE :cond
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY


See also:

* mshop/media/manager/type/search/ansi

## submanagers

List of manager names that can be instantiated by the media type manager

```
mshop/media/manager/type/submanagers = Array
(
)
```

* Default: Array
(
)

* Type: array - List of sub-manager names
* Since: 2014.03

Managers provide a generic interface to the underlying storage.
Each manager has or can have sub-managers caring about particular
aspects. Each of these sub-managers can be instantiated by its
parent manager using the getSubManager() method.

The search keys from sub-managers can be normally used in the
manager as well. It allows you to search for items of the manager
using the search keys of the sub-managers to further limit the
retrieved list of items.


## update/ansi

Updates an existing media type record in the database

```
mshop/media/manager/type/update/ansi = 
 UPDATE "mshop_media_type"
 SET :names
 	"code" = ?, "domain" = ?, "label" = ?, "pos" = ?,
 	"status" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?
```

* Default: mshop/media/manager/type/update
* Type: string - SQL statement for updating records
* Since: 2014.03

Items which already have an ID (i.e. the ID is not NULL) will
be updated in the database.

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the media type item to the statement before they are
sent to the database server. The order of the columns must
correspond to the order in the save() method, so the
correct values are bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/type/insert/ansi
* mshop/media/manager/type/newid/ansi
* mshop/media/manager/type/delete/ansi
* mshop/media/manager/type/search/ansi
* mshop/media/manager/type/count/ansi

## update/mysql

Updates an existing media type record in the database

```
mshop/media/manager/type/update/mysql = 
 UPDATE "mshop_media_type"
 SET :names
 	"code" = ?, "domain" = ?, "label" = ?, "pos" = ?,
 	"status" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?
```

* Default: 
 UPDATE "mshop_media_type"
 SET :names
 	"code" = ?, "domain" = ?, "label" = ?, "pos" = ?,
 	"status" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?


See also:

* mshop/media/manager/type/update/ansi

# update
## ansi

Updates an existing media record in the database

```
mshop/media/manager/update/ansi = 
 UPDATE "mshop_media"
 SET :names
 	"langid" = ?, "type" = ?, "label" = ?, "mimetype" = ?, "link" = ?, "status" = ?,
 	"fsname" = ?, "domain" = ?, "preview" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?
```

* Default: mshop/media/manager/update
* Type: string - SQL statement for updating records
* Since: 2014.03

Items which already have an ID (i.e. the ID is not NULL) will
be updated in the database.

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the media item to the statement before they are
sent to the database server. The order of the columns must
correspond to the order in the save() method, so the
correct values are bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/media/manager/insert/ansi
* mshop/media/manager/newid/ansi
* mshop/media/manager/delete/ansi
* mshop/media/manager/search/ansi
* mshop/media/manager/count/ansi

## mysql

Updates an existing media record in the database

```
mshop/media/manager/update/mysql = 
 UPDATE "mshop_media"
 SET :names
 	"langid" = ?, "type" = ?, "label" = ?, "mimetype" = ?, "link" = ?, "status" = ?,
 	"fsname" = ?, "domain" = ?, "preview" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?
```

* Default: 
 UPDATE "mshop_media"
 SET :names
 	"langid" = ?, "type" = ?, "label" = ?, "mimetype" = ?, "link" = ?, "status" = ?,
 	"fsname" = ?, "domain" = ?, "preview" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" LIKE ? AND "id" = ?


See also:

* mshop/media/manager/update/ansi
$columns
=====

$columns _(plural)_ represents a single column or several columns. The desired
columns may be specified using a variety of PHP data types and string formats.



`'*'` _(string containing single star character)_
-----
* If the string is a `'*'`, no processing happens, and
it is passed through to the query unmodified. This is used for `SELECT *`
statements.

PHP:
```php
$pudl->select('*', 'table');
```

Generated SQL:
```sql
SELECT * FROM `table`
```



`''` _(empty string)_
-----
* Alias of `'*'`.



`NULL`
-----
* Alias of `'*'`.



`FALSE` _(boolean)_
-----
* Alias of `'*'`.
__WARNING__ this is deprecated, and will change before PUDL 3.0



`string`
-----
* Either the name of a single column or a comma separated list of
columns inside of the string. Each column name is automatically escaped and
wrapped in backticks (or equivalent). Dots are separated out to denote the
`DATABASE.COLUMN` syntax and are wrapped properly as `` `DATABASE`.`COLUMN` ``.
_(NOTE: comma separated list syntax requires PUDL 2.9.1 or higher)_

PHP:
```php
$pudl->select('field', 'table');
$pudl->select('table.field', 'table');
$pudl->select('latitude,longitude', 'table');
$pudl->select('table.latitude,table.longitude', 'table');
```

Generated SQL:
```sql
SELECT `field` FROM `table`
SELECT `table`.`field` FROM `table`
SELECT `latitude`, `longitude` FROM `table`
SELECT `table`.`latitude`, `table`.`longitude` FROM `table`
```



`array`
-----
Each element of the array is treated as a single `string`. If the `array` index
is an `integer`, no further processing happens. If the `array` index is a
string, it is treated as a column alias in the format `` `VALUE` AS `KEY` ``. A
major difference from a normal string is that commas inside of strings are no
longer parsed, instead they are treated as part of the `identifier`.

PHP:
```php
$pudl->select(['field'], 'table');
$pudl->select(['table.field'], 'table');
$pudl->select(['latitude,longitude'], 'table');
$pudl->select(['latitude', 'longitude'], 'table');
$pudl->select(['table.latitude', 'table.longitude'], 'table');
$pudl->select(['lat'=>'latitude', 'lon'=>'longitude'], 'table');
$pudl->select(['lat'=>'table.latitude', 'lon'=>'table.longitude'], 'table');
```

Generated SQL:
```sql
SELECT `field` FROM `table`
SELECT `table`.`field` FROM `table`
SELECT `latitude,longitude` FROM `table`
SELECT `latitude`, `longitude` FROM `table`
SELECT `table`.`latitude`, `table`.`longitude` FROM `table`
SELECT `latitude` AS `lat`, `longitude` AS `lon` FROM `table`
SELECT `table`.`latitude` AS `lat`, `table`.`longitude` AS `lon` FROM `table`
```



`object` implementing `ArrayAccess`
-----
* Alias of `array`.



All other data types
-----
* Treat the value as a [`$value`](value.md).

PHP:
```php
$pudl->select(123);							// integer
$pudl->select(1.23);						// float
$pudl->select(true);						// boolean
$pudl->select(pudl::count('field'));		// pudlHelper
```

Generated SQL:
```sql
SELECT 123
SELECT 1.23
SELECT TRUE
SELECT COUNT(`field`)
```

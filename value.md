# $value

Many methods accept a __$value__ parameter, or a [__$key__ => __$value__] pair.
Here is a listing of all possible PHP values along with example implementations
with sample generated SQL.


__Table of Contents__
* [`NULL`](#null-nan-not-a-number-inf-infinite-and--inf-negative-infinite)
* [`boolean`](#boolean-true-and-false)
* [`integer`](#integer)
* [`float`](#float)
* [ASCII `string`](#ascii-encoded-string)
* [Binary `string`](#binary-string-and-utf-8-encoded-string)
* [`array` and `ArrayAccess`](#array-and-object-implementing-arrayaccess)
* [`pudlValue`](#object-implementing-pudlvalue)
* [`__toString`](#object-implementing-__tostring)




## `NULL`, `NaN` _(not a number)_, `INF` _(infinite)_ and `-INF` _(negative infinite)_


### SQL `IS NULL` for [$clause](clause.md) comparisons.
```php
/* PHP PUDL API */
$db->rows('table', ['column' => NULL]);
```
```sql
/* Generated SQL Query */
SELECT * FROM `table` WHERE (`column` IS NULL)
```


### Literal SQL `NULL` for `INSERT` and `UPDATE` data.
```php
/* PHP PUDL API */
$db->insert('table', ['column' => NULL]);
```
```sql
/* Generated SQL Query */
INSERT INTO `table` (`column`) VALUES (NULL)
```


### `NaN` treated as literal SQL `NULL` (`INF` and `-INF` do the same).
```php
/* PHP PUDL API */
$db->rows('table', ['column' => NaN]);
```
```sql
/* Generated SQL Query */
SELECT * FROM `table` WHERE (`column` IS NULL)
```




## `boolean` `TRUE` and `FALSE`


### Literal SQL `TRUE`.
```php
/* PHP PUDL API */
$db->rows('table', ['column' => TRUE]);
```
```sql
/* Generated SQL Query */
SELECT * FROM `table` WHERE (`column`=TRUE)
```


### Literal SQL `FALSE`.
```php
/* PHP PUDL API */
$db->rows('table', ['column' => FALSE]);
```
```sql
/* Generated SQL Query */
SELECT * FROM `table` WHERE (`column`=FALSE)
```




## `integer`


### Literal SQL `integer`.
```php
/* PHP PUDL API */
$db->rows('table', ['column' => 1]);
```
```sql
/* Generated SQL Query */
SELECT * FROM `table` WHERE (`column`=1)
```


### Literal SQL negative `integer`.
```php
/* PHP PUDL API */
$db->rows('table', ['column' => -5]);
```
```sql
/* Generated SQL Query */
SELECT * FROM `table` WHERE (`column`=-5)
```




## `float`


### Literal SQL `float`.
```php
/* PHP PUDL API */
$db->rows('table', ['column' => 2.3]);
```
```sql
/* Generated SQL Query */
SELECT * FROM `table` WHERE (`column`=2.3)
```


### Literal SQL `float` using scientific notation.
```php
/* PHP PUDL API */
$db->rows('table', ['column' => 1.2e23]);
```
```sql
/* Generated SQL Query */
SELECT * FROM `table` WHERE (`column`=1.2E+23)
```




## ASCII encoded `string`


### Quoted literal SQL `string`.
```php
/* PHP PUDL API */
$db->rows('table', ['column' => 'value']);
```
```sql
/* Generated SQL Query */
SELECT * FROM `table` WHERE (`column`='value')
```


### Automatically escaped and quoted literal SQL `string`.
```php
/* PHP PUDL API */
$db->rows('table', ['column' => "va'lue"]);
```
```sql
/* Generated SQL Query */
SELECT * FROM `table` WHERE (`column`='va\'lue')
```




## Binary `string` and UTF-8 encoded `string`


### Binary `string` converted to `hexadecimal` SQL literal
```php
/* PHP PUDL API */
$db->rows('table', ['column' => md5('PUDL Library',true)]);
```
```sql
/* Generated SQL Query */
SELECT * FROM `table` WHERE (`column`=0xd08be06e8daa241016e8d2b923f974f3)
```


### UTF-8 `string` converted to `hexadecimal` SQL literal
```php
/* PHP PUDL API */
$db->rows('table', ['column' => '（╯°□°）╯︵┻━┻']);
```
```sql
/* Generated SQL Query */
SELECT * FROM `table` WHERE (`column`=0xefbc88e295afc2b0e296a1c2b0efbc89e295afefb8b5e294bbe29481e294bb)
```




## `array` and `object` implementing [`ArrayAccess`](http://php.net/manual/en/class.arrayaccess.php)


### [$clause](clause.md): Recursive AND/OR (without __$key__).
When an array does not have a __$key__, it is treated as nested AND/OR blocks.
These can be nested up to 30 levels deep.
```php
/* PHP PUDL API */
$db->rows('table', [
	['column1' => 'a', 'column2' => 'b'],
	['column3' => 'c', 'column4' => 'd'],
]);
```
```sql
/* Generated SQL Query */
SELECT * FROM `table` WHERE ((`column1`='a' OR `column2`='b') AND (`column3`='c' OR `column4`='d'))
```


### [$clause](clause.md): `IN (set)` (with __$key__).
When an array does have a __$key__, the __$key__ is treated as a `column` name
with the array being treated as a list of items to search with a SQL `IN`
comparison.
```php
/* PHP PUDL API */
$db->rows('table', ['column' => ['a', 'b', 'c']]);
```
```sql
/* Generated SQL Query */
SELECT * FROM `table` WHERE (`column` IN ('a', 'b', 'c'))
```


### [$insert](insert.md): JSON string.
`INSERT` queries treat `array`s as complex data, and will convert it to a `JSON`
`string` before inserting into the database.
```php
/* PHP PUDL API */
$db->insert('table', ['column' => ['a', 'b', 'c']]);
```
```sql
/* Generated SQL Query */
INSERT INTO `table` (`column`) VALUES ('[\"a\",\"b\",\"c\"]')
```




## `object` implementing [`pudlValue`](pudlValue/pudlValue.md)


### Calls `$object->pudlValue()`.
```php
/* PHP PUDL API */
$db->rows('table', ['column' => pudl::like('value')]);
```
```sql
/* Generated SQL Query */
SELECT * FROM `table` WHERE (`column` LIKE '%value%')
```




## `object` implementing [`__toString`](http://php.net/manual/en/language.oop5.magic.php#object.tostring)


### Calls `$object->__toString()`, then processes the result the same as a [`string`](#ascii-encoded-string).
```php
/* Class with __toString() */
class MyClass {
	public function __toString() { return 'value'; }
}

$myc = new MyClass;

/* PHP PUDL API */
$db->rows('table', ['column' => $myc]);
```
```sql
/* Generated SQL Query */
SELECT * FROM `table` WHERE (`column`='value')
```




## All other values


### Examples:
* `object` (not matching `pudlValue`, `ArrayAccess`, or `__toString()`)
* `resource`
* `callable`
* `iterable`
* `void`

__Throws a `pudlTypeException`.__


```php
/* Resource PHP data type */
$file = fopen('/dev/null', 'r');

/* PHP PUDL API */
$db->rows('table', ['column' => $file]);
```
```
Uncaught pudlTypeException: Invalid data type: resource in pudl/traits/pudlRequire.php:67
Stack trace:
#0 pudl/traits/pudlQuery.php(122): pudl->_invalidType(Resource id #1)
#1 pudl/traits/pudlQuery.php(481): pudl->_value(Resource id #109, true, true)
#2 pudl/traits/pudlQuery.php(333): pudl->_clauseRecurse(Array)
#3 pudl/traits/pudlQuery.php(286): pudl->_clause(Array, 'WHERE')
#4 pudl/traits/pudlSelect.php(16): pudl->_where(Array)
#5 pudl/traits/pudlSelect.php(275): pudl->select('*', 'table', Array, false, false, false)
#6 pudl/traits/pudlSelect.php(284): pudl->selectRows('*', 'table', Array, false, false, false)
#7 test/exception.php(5): pudl->rows('table', Array)
```

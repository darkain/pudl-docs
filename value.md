# $value

Many methods accept a __$value__ parameter, or a [__$key__ => __$value__] pair.
Here is a listing of all possible PHP values along with example implementations
with sample generated SQL.




## `NULL`, `NaN` _(not a number)_, `INF` _(infinite)_ and `-INF` _(negative infinite)_
* SQL `IS NULL` for [$clause](clause.md) comparisons.
```php
$db->rows('table', ['column' => NULL]);
```
```sql
SELECT * FROM `table` WHERE (`column` IS NULL)
```

* Literal SQL `NULL` for `INSERT` and `UPDATE` data.
```php
$db->insert('table', ['column' => NULL]);
```
```sql
INSERT INTO `table` (`column`) VALUES (NULL)
```

* `NaN` treated as literal SQL `NULL` (`INF` and `-INF` do the same).
```php
$db->rows('table', ['column' => NaN]);
```
```sql
SELECT * FROM `table` WHERE (`column` IS NULL)
```




## `boolean` `TRUE` and `FALSE`
* Literal SQL `TRUE`.
```php
$db->rows('table', ['column' => TRUE]);
```
```sql
SELECT * FROM `table` WHERE (`column`=TRUE)
```

* Literal SQL `FALSE`.
```php
$db->rows('table', ['column' => FALSE]);
```
```sql
SELECT * FROM `table` WHERE (`column`=FALSE)
```





## `integer`
* Literal SQL `integer`.
```php
$db->rows('table', ['column' => 1]);
```
```sql
SELECT * FROM `table` WHERE (`column`=1)
```

* Literal SQL negative `integer`.
```php
$db->rows('table', ['column' => -5]);
```
```sql
SELECT * FROM `table` WHERE (`column`=-5)
```




## `float`
* Literal SQL `float`.
```php
$db->rows('table', ['column' => 2.3]);
```
```sql
SELECT * FROM `table` WHERE (`column`=2.3)
```

* Literal SQL `float` using scientific notation.
```php
$db->rows('table', ['column' => 1.2e23]);
```
```sql
SELECT * FROM `table` WHERE (`column`=1.2E+23)
```




## ASCII encoded `string`
* Quoted literal SQL `string`.
```php
$db->rows('table', ['column' => 'value']);
```
```sql
SELECT * FROM `table` WHERE (`column`='value')
```

* Automatically escaped and quoted literal SQL `string`.
```php
$db->rows('table', ['column' => "va'lue"]);
```
```sql
SELECT * FROM `table` WHERE (`column`='va\'lue')
```




## Binary `string` and UTF-8 encoded `string`
* Binary `string` converted to `hexadecimal` SQL literal
```php
$db->rows('table', ['column' => md5('PUDL Library',true)]);
```
```sql
SELECT * FROM `table` WHERE (`column`=0xd08be06e8daa241016e8d2b923f974f3)
```

* UTF-8 `string` converted to `hexadecimal` SQL literal
```php
$db->rows('table', ['column' => '（╯°□°）╯︵┻━┻']);
```
```sql
SELECT * FROM `table` WHERE (`column`=0xefbc88e295afc2b0e296a1c2b0efbc89e295afefb8b5e294bbe29481e294bb)
```




## `array` and `object` implementing [`ArrayAccess`](http://php.net/manual/en/class.arrayaccess.php)
* Each method handles this differently. Please see each method's
documentation.
* [$clause](clause.md): recursive AND/OR (without __$key__)
* [$clause](clause.md): `IN (set)` (with __$key__)
* [$insert](insert.md): JSON string.
* [$update](update.md): JSON merge.




## `object` implementing [`pudlValue`](pudlValue/pudlValue.md)
* Calls `$object->pudlValue()`.
```php
$db->rows('table', ['column' => pudl::like('value')]);
```
```sql
SELECT * FROM `table` WHERE (`column` LIKE '%value%')
```




## `object` implementing [`__toString`](http://php.net/manual/en/language.oop5.magic.php#object.tostring)
* Calls `$object->__toString()`, then processes same as a [`string`](#ascii-encoded-string).




## All other values (eg: `object` not matching above, `resource`, `callable`, `iterable`, and `void`)
* Throws a `pudlValueException`.

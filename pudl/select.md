# SELECT

These are the basic long-form methods that closest match raw SQL. Most other
methods rely heavily upon these, but can also be called directly from the
application layer.


```php
$result = $db->select($column [,$table=false] [,$clause=false] [,$order=false] [,$limit=false] [,$offset=false]);
// SELECT {$column} [FROM {$table}] [WHERE ($clause)] [ORDER BY {$order}] [LIMIT {$limit}{,$offset}]
// returns a pudlResult instance
```


```php
$result = $db->having($column, $table [,$clause=false] [,$having=false] [,$order=false] [,$limit=false] [,$offset=false]);
// SELECT {$column} FROM {$table} [WHERE ($clause)] [HAVING ($having)] [ORDER BY {$order}] [LIMIT {$limit}{,$offset}]
// returns a pudlResult instance
```


```php
$result = $db->group($column, $table [,$clause=false] [,$group=false] [,$order=false] [,$limit=false] [,$offset=false]);
// SELECT {$column} FROM {$table} [WHERE ($clause)] [GROUP BY ($group)] [ORDER BY {$order}] [LIMIT {$limit}{,$offset}]
// returns a pudlResult instance
```


```php
$result = $db->groupHaving($column, $table [,$clause=false] [,$group=false] [,$having=false] [,$order=false] [,$limit=false] [,$offset=false]);
// SELECT {$column} FROM {$table} [WHERE ($clause)] [GROUP BY ($group)] [HAVING ($having)] [ORDER BY {$order}] [LIMIT {$limit}
// returns a pudlResult instance
```


```php
$result = $db->distinct($column, $table [,$clause=false] [,$order=false] [,$limit=false] [,$offset=false]);
// SELECT DISTINCT {$column} FROM {$table} [WHERE ($clause)] [ORDER BY {$order}] [LIMIT {$limit}{,$offset}]
// returns a pudlResult instance
```


```php
$row = $db->selectRow($column, $table [,$clause=false] [,$order=false], $limit=1 [,$offset=false]);
// SELECT {$column} FROM {$table} [WHERE ($clause)] [ORDER BY {$order}] [LIMIT {$limit}{,$offset}]
// returns an (array) of the given row
```


```php
$row = $db->row($table [,$clause=false] [,$order=false]);
// SELECT * FROM {$table} [WHERE ($clause)] [ORDER BY {$order}] LIMIT 1
// returns an (array) of the given row
```


```php
$row = $db->rowEx($column, $table [,$clause=false] [,$order=false]);
// SELECT {$column} FROM {$table} [WHERE ($clause)] [ORDER BY {$order}] LIMIT 1
// returns an (array) of the given row
```


```php
$row = $db->rowId($table, $column [,$id=false]);
// SELECT * FROM {$table} WHERE ({$column}={$id}) LIMIT 1
// returns an (array) of the given row
```


```php
$rows = $db->selectRows($col, $table [,$clause=false] [,$order=false] [,$limit=false] [,$offset=false]);
// SELECT {$column} FROM {$table} [WHERE ($clause)] [ORDER BY {$order}] [LIMIT {$limit}{,$offset}]
// returns an (array) of multiple row (arrays)
```


```php
$rows = $db->rows($table [,$clause=false] [,$order=false]);
// SELECT * FROM {$table} [WHERE ($clause)] [ORDER BY {$order}]
// returns an (array) of multiple row (arrays)
```


```php
$rows = $db->rowId($table, $column [,$id=false]);
// SELECT * FROM {$table} WHERE ({$column}={$id})
// returns an (array) of multiple row (arrays)
```

There is also the more complex `selex` method which is also used by `pudlOrm`
and other internal features. The `selex` method takes in an associative (array)
with each of the query sections being optional. Parameters that are omitted from
the (array) will not appear in the generated SQL query. Each of the (array) keys
listed below are all optional. The `selex` method returns an instance of
[`pudlResult`](pudlResult.md).


```php
$result = $db->selex([
	// [SELECT {column}]
	// if omitted or empty becomes [SELECT *]
	'column'	= '',

	// [FROM {table}]
	// if omitted, SQL error may be generated
	'table'		= '',

	// [WHERE (clause)]
	'clause'	= '',

	// [GROUP BY {group}]
	'group'		= '',

	// [HAVING (having)]
	'having'	= '',

	// [ORDER BY (order)]
	'order'		= '',

	// [LIMIT {$limit}{,$offset}]
	'limit'		= '',
	'offset'	= '',
]);
```

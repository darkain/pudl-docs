* `boolean` `false` 2.9.0 - No clause processing happens. (deprecated)

* `NULL` 2.9.1 - No clause processing happens.

* `object` - Same as `array`.

* Nested `array` - Recursive `AND` / `OR` comparison.

* `array` - If key is an `integer`, the value is passed directly to SQL as a
comparison. If key is a `string`, the key is treated as a column name and the
value is treated as a `$value` listed above. If value is an `array` however, it
is treated like an `IN (list)` comparison. If value


```php
// Compare two columns
$clause = ['column_a = column_b'];
// SQL: (`column_a`=`column_b`)
```
```php
// Compare a column to a string value
$clause = ['column_a' => 'value_b'];
// SQL: (`column_a`='value_b')
```
```php
// Compare a column to a string value
$clause = ['column_a' => ['1,2,3'];
// SQL: (`column_a` IN ('1,2,3'))
```
```php
// Compare a column to a collection of string values
$clause = ['column_a' => ['1', '2', '3'];
// SQL: (`column_a` IN ('1', '2', '3'))
```
```php
// Compare a column to NULL
$clause = ['column_a' => NULL];
// SQL: (`column_a` IS NULL)
```
```php
// Compare two columns to values with an OR condition between them
$clause = [ // AND (only 1 item)
	[ // OR (2 items)
		'column_a' => 1,
		'column_b' => 2,
	],
];
// SQL: ((`column_a`=1) OR (`column_b`=2))
```
```php
// Complex AND/OR comparision
$clause = [ // AND (only 1 item)
	[ // OR (2 items)
		'column_a' => 1,
		[ // AND (2 items)
			'column_b' => 2,
			'column_c' => 3,
		],
	],
];
// SQL: ((`column_a`=1) OR ((`column_b`=2) AND (`column_c`=3)))
```


`TODO: add documentation for pudlHelper objects`

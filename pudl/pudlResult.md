# pudlResult


The `pudlResult` is the main object instance returned by most `pudl` API calls.
This object supports most common and standard features found in other SQL
drivers, with a few additional features geared specifically for `pudl`. Various
PHP language features are also supported by the `pudlResult` object as
demonstrated below.


```php
// Get rows using variable-function syntax
while ($data = $result()) {
	var_dump($data);
}


// Get rows using foreach syntax
foreach ($result as $data) {
	var_dump($data);
}


// Get rows using object-method syntax
while ($data = $result->row()) {
	var_dump($row);
}


// Get all rows at once
$rows = $result->rows();


// Get all rows as a JSON string
$json = $result->json();
```

Once usage of the result is finished, it is a good idea to call `free()` on the
`pudlObject` instance so that way it no longer holds on to the resource
allocation. If this isn't called manually, resources will be freed at the end
of the current running PHP script automatically. However, if there are many
`pudl` calls without freeing resources, there is a chance of hitting PHP's
defined memory limit. Luckily, there are also shortcut functions to get the row
data and free the `pudlObject` resource within a single call to make this
process more elegant.

```php
// Same as calling $result->rows(); $result->free();
$rows = $result->complete();


// Same as calling $result->complete(), for key/value pairs (2 column SQL result sets)
$rows = $result->collection();


// Same as calling $result->json(); $result->free();
$json = $result->completeJson();


// Can also be used on pudl calls that return a $result
$rows = $db->select('*', 'table')->complete();


// Oh, and of course JSON too!
$json = $db->select('*', 'table')->completeJson();
```

There are a few more helpful methods for `pudlObject` as well.

```php
// Get the query that generated this $result set
$query = $result->query();
```
```php
// Check if there was an error code with this query
$error = $result->error();
```
```php
// Get the number of rows in the $result set
$int = $result->count();
// or
$int = count($result);
```
```php
// Get if there are rows in the $result set
$bool = $result->hasRows();
```
```php
// Move the internal row pointer to the 10th row in the $result set
$result->seek(10);
```
```php
// Move the internal row pointer to the first row in the $result set
$result->rewind();
// or
rewind($result);
```
```php
// Check if the internal row pointer is point to a valid row
$bool = $result->valid();
```
```php
// Get the internal row pointer
$int = $result->key();
// or
$int = key($result);
```
```php
// Get the current row in the $result set without moving the internal row pointer
$row = $result->current();
// or
$row = current($result);
```
```php
// Move the internal row pointer to the next row and return that row
$row = $result->next();
// or
$row = next($result);
// or
$row = $result();
// or
$row = $result->row();
```
```php
// Get the number of column fields in the $result set
$int = $result->fields();
```
```php
// Get information on a particular column field in the $result set
$data = $result->getField($column);
```
```php
// Get information on all column fields in the $result set
$data = $result->listFields();
```

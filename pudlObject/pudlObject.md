# class: pudlObject

## Overview
**pudlObject** is a wrapper class for PHP's built in array data type in order to access it using object syntax notation. This object also adds a few additional custom methods for a few specific needs within PUDL as a whole.

### Implements
* [ArrayAccess](http://php.net/manual/en/class.arrayaccess.php)
* [pudlData](../pudlData)

### Extended By
* [pudlCollection](../pudlCollection)
* pudlImport
* [pudlOrm](../pudlOrm)

## Methods

### public function \_\_construct(&$data=NULL, $process=false)

### public function \_\_debugInfo()

### public function &\_\_get($key)

### public function \_\_isset($key)

### public function \_\_set($key, $value)

### public function \_\_unset($key)

### public function append($array)

### public function appendInto(&$array)

### public function arsort($sort_flags=SORT_REGULAR)

### public function asort($sort_flags=SORT_REGULAR)

### public function compareData()

### public function compareSnap()

### public function copy($data)

### public function count()

### public function current()

### public function diff()

### public function diff_assoc()

### public function diff_assoc_recursive()

### public function diff_key()

### public function each($callback)

### public function extend($source, $keys)

### public function extract($keys)

### public function fields()

### public function flip()

### public function free()

### public function getField($column)

### public function govern(&$data)

### public function has($key, $value=true)

### public function implode($glue=',')

### public function in($value, $strict=false)

### public function inject($offset, $items)

### public function intersect()

### public function intersect_assoc()

### public function intersect_key()

### public function json()

### public function key()

### public function keys($search_value=null, $strict=false)

### public function krsort($sort_flags=SORT_REGULAR)

### public function ksort($sort_flags=SORT_REGULAR)

### public function listFields()

### public function merge($array)

### public function mergeInto(&$array)

### public function mergeRecursive($array)

### public function next()

### public function offsetExists($key, $isset=true)

### public function &offsetGet($key)

### public function offsetSet($key, $value)

### public function offsetUnset($key)

### public function partition($columns)

### public function pop()

### public function push()

### public function &raw()

### public function replace($array)

### public function replaceRecursive($array)

### public function reverse($preserve_keys=true)

### public function rewind()

### public function row($type=PUDL_ARRAY)

### public function rsort($sort_flags=SORT_REGULAR)

### public function seek($row)

### public function shift()

### public function shuffle()

### public function slice($offset, $length=NULL, $preserve_keys=false)

### public function snapshot($snapshot=true)

### public function sort($sort_flags=SORT_REGULAR)

### public function splice($offset, $length=NULL, $replacement)

### public function unshift()

### public function valid()

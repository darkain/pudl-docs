# Interface: pudlData

## Overview

### Extends
* [Countable](http://php.net/manual/en/class.countable.php)
* [SeekableIterator](http://php.net/manual/en/class.seekableiterator.php)

### Implemented By
* [pudlObject](../pudlObject)
* [pudlResult](../pudlResult.md)

## Methods

### public function count();
[Countable::count — Count elements of an object](http://php.net/manual/en/countable.count.php)

### public function current();
[Iterator::current — Return the current element](http://php.net/manual/en/iterator.current.php)

### public function fields();
Return the total number of fields available for the data.

### public function free();
Releases all resources consumed by this object and returns it back to its default empty state.

### public function getField($column);
Returns information about a specific field based on a $column identifier.

### public function json();
Gets a JSON text object representation of this object's data

### public function key();
[Iterator::key — Return the key of the current element](http://php.net/manual/en/iterator.key.php)

### public function listFields();
Returns a list of all fields available for the given object's data.

### public function next();
[Iterator::next — Move forward to next element](http://php.net/manual/en/iterator.next.php)

### public function rewind();
[Iterator::rewind — Rewind the Iterator to the first element](http://php.net/manual/en/iterator.rewind.php)

### public function row($type=PUDL_ARRAY);
Returns the current row data and advances the internal row pointer to the next available row data.

### public function seek($position);
[SeekableIterator::seek — Seeks to a position](http://php.net/manual/en/seekableiterator.seek.php)

### public function valid();
[Iterator::valid — Checks if current position is valid](http://php.net/manual/en/iterator.valid.php)
* `string` - The name of a single SQL table or a comma separated list of tables.
(NOTE: comma separated list syntax requires PUDL 2.9.1 or higher)

* `object` implementing `ArrayAccess` - Same as `array` listed below.

* Anything else - throws a `pudlValueException`

* `array`
Each element within the array is a different `TABLE` that are `JOIN`ed by
default using the `,` (comma) `JOIN` syntax. If `array` keys are `integer`s,
`table` names are processed as-is. If `array` keys are `string`s, then `table`
names are aliased using the ``value` AS `key`` SQL syntax.

`TODO: add documentation for complex array/join syntax`

* `string` value `'*'` - If the string is a `'*'`, no processing happens, and
it is passed through to the query unmodified. This is used for `SELECT *`
statements.

* `string` value `''` (empty string) - Same as `'*'`.

* `NULL` - Same as `'*'`.

* `false` 2.9.0 - Same as `'*'`. (deprecated)

* `string` - Either the name of a single column or a comma separated list of
columns inside of the string. Each column name is automatically escaped and
wrapped in backticks (or equivalent). Dots are separated out to denote the
`DATABASE.COLUMN` syntax and are wrapped properly as ``DATABASE`.`COLUMN``.
(NOTE: comma separated list syntax requires PUDL 2.9.1 or higher)

* `array` - Each element of the array is treated as a single `string` as
mentioned above. If the `array` index is an `integer`, no further processing
happens. if the `array` index is a string, it is treated as a column alias in
the format ``VALUE` AS `KEY``.

* `object` implementing `ArrayAccess` - Same as `array`.

* All other types - treat the value as a [`$value`](value.md).

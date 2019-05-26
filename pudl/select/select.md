Execute a SELECT statement and return a pudlResult instance containing the resulting rows.

```php
$result = $db->select($column [,$table=false] [,$clause=false] [,$order=false] [,$limit=false] [,$offset=false]);
// SELECT {$column} [FROM {$table}] [WHERE ($clause)] [ORDER BY {$order}] [LIMIT {$limit}{,$offset}]
// returns a pudlResult instance
```


Example 1:
```php
$result = $db->select(
    ['id', 'user', 'about'],
    'users',
    ['access' => 'admin']
);
```
This will execute:
```sql
SELECT `id`, `user`, `about` FROM `users` WHERE `access`='admin'
```

Identifiers such column and table names are automatically encased and values are automatically escaped when needed.

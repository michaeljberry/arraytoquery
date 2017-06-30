# querybuilder
Take PHP arrays and convert to SQL

## Purpose
The purpose of this project is to convert PHP arrays to valid SQL. The goal is to make it as easy and simple as possible to write an array and convert it to SQL. Error checking has been kept to a minimum except for the most logical errors; i.e. trying to group by a column in a table that wasn't originally selected or joined. Some conventions have been used to standardize the order in which arrays are created and parsed. It supports sub-queries through recursion. It also supports prepared statement bindings through the usual `?` or `:{placeholder}`.

### How to use
You first need an array of SQL statements. There are many supported formats of the information, however, they all follow the same flow. You begin with an array:

```php
$sql = [];
```

Then you can begin adding your statements. If you want to create a `SELECT` statement, your first array key will be:

```php
$sql = [
  'SELECT' => []
];
```

You will use this same structure to add `JOIN`, `WHERE`, `GROUP BY`, and `ORDER BY` statements. For example:

```php
$sql = [
  'SELECT' => [],
  'JOIN' => [],
  'WHERE' => [],
  'GROUP BY' => [],
  'ORDER BY' => [],
];
```

Now to the nitty-gritty. You will add keys and values in mostly the same way that you would write a typical SQL statement. Here's an example query that I had and following will be the array-ized (I think that's a word! :D) version:

```sql
SELECT os.order_id, os.type, oi.item_id, os.processed 
FROM order_sync os 
JOIN sync.order so ON so.order_num = os.order_id 
JOIN order_item oi ON oi.order_id = so.id 
WHERE track_successful IS NULL AND so.cancelled IS NULL ORDER BY os.processed ASC
```

{More instructions to come...}

You'd take your array and pass it to:

`\QB\querybuilder::arrayToQuery($sql)`



### Input -
```js
await pool.query(sqlString, arraysOfValues);
```

### Output -
```js
{
  rows: [ { id: 1, username: 'sarthak' } ],
  // 1. The actual data (Array of Objects)
  rowCount: 1,
  // 2. Total number of rows affected/returned (Number)
  command: 'SELECT'
  // 3. The type of SQL command run (String)
}
```


### returning * - for `INSERT` or `UPDATE` queries
```js
// Without RETURNING, result.rows will be empty []
postgres m kam ho jaega but vo return automatic thodi karega, islie ->

const result = await pool.query(
  'INSERT INTO users(username) VALUES($1) RETURNING *', 
  ['sarthak']
);
// Now result.rows[0] contains the new user object with its auto-generated ID!
```


[[SQL -]]
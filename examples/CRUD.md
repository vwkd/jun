# CRUD



## Create

```
struct Users {
  id: u128,
  name: String,
  age: u8,
}

markPrimaryKey(Users::id);
```

```sql
CREATE TABLE users (
  id INT PRIMARY KEY,
  name TEXT,
  age INT
);
```



## Read

- read some

```
use Users;

if id == 1 {
  id, name
}
```

```sql
SELECT id, name
FROM users
WHERE id = 1;
```

- read all

```
use Users;

if id == 1 {
  _
}
```

```sql
SELECT *
FROM users
WHERE id = 1;
```



## Update

```
use Users;

if id == 1 {
  age = 42;
}
```

```sql
UPDATE users
SET age = 42
WHERE id = 1;
```



## Insert

```
use Users;

if id == None {
  id = 1;
  name = "John Doe";
  age = 42;
}
```

```sql
INSERT INTO users (id, name, age)
VALUES (1, 'John Doe', 42);
```



## Delete

```
use Users;

if id == 1 {
  _ = None;
}
```

```sql
DELETE FROM users
WHERE id = 1;
```

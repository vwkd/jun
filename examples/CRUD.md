# CRUD



## Schema

```
type Movie {
  title: String!,
  actors: [Actor!],
}

type Actor {
  name: String!
}
```

```sql
CREATE TABLE Movie (
  id INT PRIMARY KEY,
  title TEXT NON NULL,
);

CREATE TABLE Actor (
  id INT PRIMARY KEY,
  name TEXT NON NULL,
);

CREATE TABLE MovieActor (
  id INT PRIMARY KEY,
  movie_id INT NON NULL,
  actor_id INT NON NULL,
);
```



## Create

```
Movie {
  title: "Dune",
  actors: [
    Actor {
      name: "Timothée Chalamet",
    },
    Actor {
      name: "Zendaya",
    }
  ]
}
```

```sql
INSERT INTO Movie (id, title) VALUES (1, 'Dune');

INSERT INTO Actor (id, name) VALUES (1, 'Timothée Chalamet');
INSERT INTO Actor (id, name) VALUES (2, 'Zendaya');

INSERT INTO MovieActor (id, movie_id, actor_id) VALUES (1, 1, 1);
INSERT INTO MovieActor (id, movie_id, actor_id) VALUES (2, 1, 2);
```



## Read

- without filter

```
Movie {
  title,
  actors {
    name,
  },
}
```

```sql
SELECT
  JSON_OBJECT(
    'title', M.title,
    'actors', JSON_ARRAYAGG(JSON_OBJECT('name', A.name))
  ) AS movie_data
FROM
  Movie M
INNER JOIN
  MovieActor MA ON M.id = MA.movie_id
INNER JOIN
  Actor A ON MA.actor_id = A.id
GROUP BY
  M.title;
```

- with filter

```
Movie {
  title,
  actors {
    name,
  },
}
.filter(id != uuid("123"))
.sort(title)
.skip(10)
.take(10)
```

```sql
SELECT
  JSON_OBJECT(
    'title', M.title,
    'actors', JSON_ARRAYAGG(JSON_OBJECT('name', A.name))
  ) AS movie_data
FROM
  Movie M
INNER JOIN
  MovieActor MA ON M.id = MA.movie_id
INNER JOIN
  Actor A ON MA.actor_id = A.id
WHERE
  M.id <> 123
GROUP BY
  M.title
ORDER BY
  M.title
LIMIT 10
OFFSET 10;
```



## Update

```
Movie {
  title: "Dune 1",
}
.filter(id == uuid("123"))
```

```sql
UPDATE Movie
SET title = 'Dune 1'
WHERE id = 123;
```



## Delete

```
Movie
.filter(id == uuid("123"))
.delete()
```

```sql
DELETE FROM Movie
WHERE id = 123;
```

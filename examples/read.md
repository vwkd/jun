# Read



## Simple

```
Movie {
  title,
  actors {
    name,
  },
}
if {
  id != uuid("123")
}
sort {
  title
}
skip {
  10
}
take {
  10
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
WHERE
  M.id <> 1
GROUP BY
  M.title
ORDER BY
  M.title
LIMIT 10
OFFSET 10;
```

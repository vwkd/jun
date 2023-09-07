# Schema



## Simple

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

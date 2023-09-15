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
  title TEXT NOT NULL,
);

CREATE TABLE Actor (
  id INT PRIMARY KEY,
  name TEXT NOT NULL,
);

CREATE TABLE MovieActor (
  id INT PRIMARY KEY,
  movie_id INT NOT NULL REFERENCES Movie(id),
  actor_id INT NOT NULL REFERENCES Actor(id),
);
```

```esdl
type Movie {
  required title: str;
  multi actors: Actor;
}

type Actor {
  required name: str;
}
```

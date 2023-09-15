# Create



## Simple

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

```edgeql
insert Movie {
  title := "Dune",
  actors := {
    (insert Actor {
      name := "Timothée Chalamet"
    }),
    (insert Actor {
      name := "Zendaya"
    })
  }
};
```

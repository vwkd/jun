# Update



## Simple

```
Movie {
  title: "Dune 1",
}
if {
  id == uuid("123")
}
```

```sql
UPDATE Movie
SET title = 'Dune 1'
WHERE id = 1;
```

# Delete



## Simple

```
delete Movie
if {
  id == uuid("123")
}
```

```sql
DELETE FROM Movie
WHERE id = 1;
```

```edgeql
delete Movie
filter .id = <uuid>"123";
```

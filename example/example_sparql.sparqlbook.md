
```sparql
select (count(*) as ?number)
where {
dbr:List_of_archaeologists dbo:wikiPageWikiLink ?s.
?s a dbo:Person
}
LIMIT 100
```

```sparql
select ?s
where {
dbr:List_of_archaeologists dbo:wikiPageWikiLink ?s.
?s a dbo:Person
}
LIMIT 100
```

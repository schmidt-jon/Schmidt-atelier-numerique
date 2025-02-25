---
title: "Example-Sparqlbook"
author: "Jonathan"
date: "2025-02-25"
output: html_document
---
This is my SPARQL example notebook to do SPARQL queries. It also works as documentation
for my general workflow.
Saved a new file as .sparqlbook and then exported it to .md (Markdown). 

Github Link:  Git Line du command: MINGW64

SPARQL queries in markdown are signified as 
#```sparql
#```
Between it follows a slight variation of standard SQL quaries with following changes:
a = rdf.type
?s = variable
count: select (count(*) as ?number)
where clause inside {}
Order inside where clause (normally): Subject Prädikat Objekt
--> ?s (variable == Subject) dbo:??? (RDF Type == Prädikat) dbr:??? (RDF Object == Objekt)

Example queries are (with reverse SPO -- Object Prädikat Subjekt):

Number of Archaeologists who appear in "List_of_archaeologists"
```sparql
select (count(*) as ?number) #Just the number of results
where {
dbr:List_of_archaeologists dbo:wikiPageWikiLink ?s. #reversed order. Clause not finished: . at the end works as AND
?s a dbo:Person #filters to only pages of persons
}
LIMIT 100
```
Show first hundred List_of_archaeologists:
```sparql
select ?s #Select as Variable
where {
dbr:List_of_archaeologists dbo:wikiPageWikiLink ?s. #Variable that appear on the registry wikiPageWikiLink in the List_of_archaeologists
?s a dbo:Person #and are persons
}
LIMIT 100 #limit query!
```
Show which attributes appear how often in the List_of_archaeologists (ontoly important)
```sparql
PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/>
SELECT ?p1 (COUNT(*) as ?eff) 
WHERE { 
dbr:List_of_archaeologists ?p ?o1.
?o1 a dbo:Person;
    ?p1 ?o2.
  }
GROUP BY ?p1
ORDER BY DESC(?eff)
```

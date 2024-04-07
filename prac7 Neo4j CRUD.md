*Create nodes for persons*

```javascript
CREATE (:Person {name: 'Asad'})
CREATE (:Person {name: 'Deep'})
CREATE (:College {name: 'Mithibai'})
CREATE (:College {name: 'Wilson'})
```

||creating relation ship between nodes||
```javascript
match (a:Person),(b:College) where a.name="Asad" and b.name="Mithibai" create(a)-[:studyin]->(b)
match (a:Person),(b:College) where a.name="Deep" and b.name="Wilson" create(a)-[:studyin]->(b)
match (a:Person),(b:Person) where a.name="Deep" and b.name="Asad" create(a)-[:friend]->(b)
```


|finding nodes|
```javascript
match (a:Person) return a #shows all person in graph view
match (a:Person) return a.name #shows all person in table form
```

|updating age|
```javascript
match (a:Person{name:"Asad"}) set a.age=20 #add peroperty age=20
match (a:Person{name:"Deep"}) set a.age=21 
```

|finding by age|
```javascript
match (a:Person) where a.name="Deep" return a.age #table view
match (a:Person) where a.name="Deep" return a #node view
```

|deleting node|
```javascript
deleting node requires detaching of relatinoship
match (a:Person) where a.name="Deep" detach delete a #detaching relationship and deleting the node
MATCH (n:Person {name: 'Asad'})-[r:studyin]->() DELETE r #detaching relation ship
```

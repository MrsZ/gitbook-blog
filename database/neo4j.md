Start

sandbox: [https://neo4j.com/sandbox-v2/](https://neo4j.com/sandbox-v2/)

docker: [https://hub.docker.com/\_/neo4j/](https://hub.docker.com/_/neo4j/)

```bash
docker run -d --publish=7474:7474 --publish=7687:7687 --volume=$HOME/neo4j/data:/data neo4j
```

Migrate from relational database

Workbench export data to CSV

basic grammar

```bash
CREATE (ee:Person { name: "Emil", from: "Sweden", klout: 99 })
```

* `CREATE` clause to create data
* `()` parenthesis to indicate a node
* `ee:Person` a variable 'ee' and label 'Person' for the new node
* `{}`brackets to add properties to the node

```
MATCH (ee:Person) WHERE ee.name = "Emil" RETURN ee;
```

* `MATCH`clause to specify a pattern of nodes and relationships

* `(ee:Person)`a single node pattern with label 'Person' which will assign matches to the variable 'ee'

* `WHERE`clause to constrain the results

* `ee.name = "Emil"`compares name property to the value "Emil"

* `RETURN`clause used to request particular results

```
MATCH (ee:Person)-[:KNOWS]-(friends) WHERE ee.name = "Emil" RETURN ee, friends
```

* `MATCH`clause to describe the pattern from known Nodes to found Nodes
* `(ee)`starts the pattern with a Person \(qualified by WHERE\)
* `-[:KNOWS]-`matches "KNOWS" relationships \(in either direction\)
* `(friends)`will be bound to Emil's friends

```bash
MATCH (js:Person)-[:KNOWS]-()-[:KNOWS]-(surfer)
WHERE js.name = "Johan" AND surfer.hobby = "surfing"
RETURN DISTINCT surfer
```

* `()`empty parenthesis to ignore these nodes

* `DISTINCT`because more than one path will match the pattern

* `surfer`will contain Allison, a friend of a friend who surfs

显示语句执行过程 EXPLAIN或者PROFILE

```
PROFILE MATCH (js:Person)-[:KNOWS]-()-[:KNOWS]-(surfer)
WHERE js.name = "Johan" AND surfer.hobby = "surfing"
RETURN DISTINCT surfer
```




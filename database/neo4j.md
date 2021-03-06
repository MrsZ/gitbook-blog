# Conceot

* Nodes：基本节点
* labels： 类似于node的类型
* relationships：节点间的关系
* properties：节点的属性

Start

sandbox: [https://neo4j.com/sandbox-v2/](https://neo4j.com/sandbox-v2/)

docker: [https://hub.docker.com/\_/neo4j/](https://hub.docker.com/_/neo4j/)

```bash
docker run -d --publish=7474:7474 --publish=7687:7687 --volume=$HOME/neo4j/data:/data neo4j
```

# Migrate from relational database

Workbench export data to CSV

[https://dzone.com/refcardz/from-relational-to-graph-a-developers-guide](https://dzone.com/refcardz/from-relational-to-graph-a-developers-guide)

```bash
load csv with headers from "file:///v3_user.csv" as row
create (n:User)
SET n = row
```

# Basic grammar

\(\) for node

\[\] for relation

{} for properties

* MATCH
* CREATE
* RETURN
* WITH: pipe the result
* ```bash
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

Query all nodes

```bash
MATCH (n)
RETURN n
```

delete nodes and its relationship

```
MATCH (emil:Person {name:"Emil Eifrem"})
OPTIONAL MATCH (emil)-[r]-()
DELETE emil,r
```

create nodes with constraints

```
CREATE CONSTRAINT ON (flight:Flight) ASSERT flight.code IS UNIQUE;
```

iterator path

6 hop

```
MATCH path = (london:City{name:'London'})-[:HAS_FLIGHT|FLYING_TO*0..6]->(melbourne:City{name:'Melbourne'}) RETURN path;
```

tutorial

[https://neo4j.com/graphacademy/online-training/getting-started-graph-databases-using-neo4j/part-1/](https://neo4j.com/graphacademy/online-training/getting-started-graph-databases-using-neo4j/part-1/)


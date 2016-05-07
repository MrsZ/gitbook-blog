# Graph Database


## Cypher
Cypher: graph database query language  
examples
```
(emil)<-[:KNOWS]-(jim)-[:KNOWS]->(ian)-[:KNOWS]->(emil)
```
```
MATCH (a:Person {name:'Jim'})-[:KNOWS]->(b)-[:KNOWS]->(c),
      (a)-[:KNOWS]->(c)
RETURN b, c
```
```
MATCH (a:Person)-[:KNOWS]->(b)-[:KNOWS]->(c), (a)-[:KNOWS]->(c)
WHERE a.name = 'Jim'
RETURN b, c
```

## Neo4j
configuration on vagrant. https://github.com/bretcope/vagrant-neo4j  

###py2neo
Create nodes and relationship
```python
from py2neo import authenticate, Graph, Node
# authorize the client
authenticate("localhost:7474", "neo4j", "password")
graph = Graph()
# clear the database first
graph.delete_all()
# create Node
nicole = Node("Person", name="Nicole", age=24)
# add node to the graph
graph.create(nicole)
# create another node
bar = Node("Bar", name="Kingfish")
graph.create(bar)
# Create relationship
from py2neo import Relationship
rel = Relationship(nicole, "LIKES", bar, since=2014)
# add to graph
graph.create(rel)
```

merge node  
merge_one function is used to create node when you do not know whether it exist in the database
```python
# will create a new node with the same name nicole
nicole = Node("Person", name="Nicole")
graph.create(nicole)
graph.delete(nicole)

# will not create a new node
nicole = graph.merge_one("Person", "name", "Nicole")
graph.create(nicole)

# create a new node kenny
kenny = graph.merge_one("Person", "name", "Kenny")
graph.create(kenny)

# if the node not exist, the function will return none
# thus kingfish == none, and graph.create function will return errors
kingfish = graph.find_one("Bar", "name", "Kingfish")
graph.create(kingfish)

```

Merge relationships
```python
nicole = graph.find_one("Person", "name", "Nicole")
kenny = graph.find_one("Person", "name", "Kenny")
kingfish = graph.find_one("Bar", "name", "Kingfish")

# will create a new relationship
rel = Relationship(nicole, "LIKES", kingfish)
graph.create(rel)

# will only create one relationship
rel = Relationship(kenny, "LIKES", kingfish)
graph.create_unique(rel)
rel = Relationship(kenny, "LIKES", kingfish)
graph.create_unique(rel)
```

cypher query  
delete all before data and use Movie example
```sql
MATCH (p:Person)-[:PRODUCED]->(m:Movie)
RETURN p.name AS name, m.title AS movie
```
```python
data = graph.cypher.execute("MATCH (p:Person)-[:PRODUCED]->(m:Movie) RETURN p.name AS name, m.te AS movie")
type(data)
type(data[0])
data
data[0]
data[0].name
data[0]["name"]
```

Parameterized Cypher
```python
query = "MATCH (p:Person)-[:ACTED_IN]->(m:Movie) WHERE m.title = {movie} RETURN p.name"
graph.cypher.execute(query, {"movie": "The Matrix"})
```

Graph Versus Tabular Cypher
```python
data = graph.cypher.execute("MATCH (p:Person)-[:PRODUCED]->(m:Movie) RETURN p, m")
```

Set constraint and Index
```python
graph.cypher.execute("CREATE CONSTRAINT ON {n:User} ASSER n.username IS UNIQUE")
graph.cypher.execute("CREATE CONSTRAINT ON {n:Post} ASSER n.username IS UNIQUE")
graph.cypher.execute("CREATE CONSTRAINT ON {n:Tag} ASSER n.username IS UNIQUE")
```

### Use Case

#### Register and Login
每个用户是一个Node, node的label为User, 有两个属性username和password, password需要加密
```python
class User:

    def __init__(self, username):
        self.username = username

    def find(self):
        user = graph.find_one("User", "username", self.username)
        return user

    def register(self, password):
        if not self.find():
            user = Node("User", username=self.username, password=bcrypt.encrypt(password))
            graph.create(user)
            return True

        return False

    def verify_password(self, password):
        user = self.find()

        if not user:
            return False

        return bcrypt.verify(password, user["password"])
```
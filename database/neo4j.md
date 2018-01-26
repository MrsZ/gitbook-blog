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
* `{} `brackets to add properties to the node




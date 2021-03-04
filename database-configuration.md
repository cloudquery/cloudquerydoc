# Database Configuration

cloudquery currently supports two types of databases: **Relational** - PostgreSQL and **graph** - Neo4j.

### Relational

{% tabs %}
{% tab title="PostgreSQL" %}
```bash
./cloudquery fetch --driver postgresql --dsn "host=localhost user=postgres password=pass DB.name=postgres port=5432"
```

To run a local PostgreSQL instance via [docker](https://hub.docker.com/_/postgres):

```bash
docker run -p 5432:5432 -e POSTGRES_PASSWORD=pass -d postgres
```
{% endtab %}

{% tab title="Neo4j" %}
```bash
./cloudquery fetch --driver neo4j --dsn "neo4j://neo4j:pass@localhost:7687"
```

To run a local Neo4j instance via [docker](https://hub.docker.com/_/neo4j):

```bash
docker run \
    -p7474:7474 -p7687:7687 \
    -d \
    -v $HOME/neo4j/data:/data \
    -v $HOME/neo4j/logs:/logs \
    -v $HOME/neo4j/import:/var/lib/neo4j/import \
    -v $HOME/neo4j/plugins:/plugins \
    --env NEO4J_AUTH=neo4j/pass \
    neo4j:latest
```
{% endtab %}

{% tab title="Other" %}
Wanna see support for other graph database? Please open an [issue](https://github.com/cloudquery/cloudquery/issues):\)
{% endtab %}
{% endtabs %}




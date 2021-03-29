# Database Configuration

cloudquery currently supports two types of databases: **Relational** - SQLite, MySQL, PostgreSQL, SQL Server and **graph** - Neo4j.

## Relational

{% tabs %}
{% tab title="SQLite" %}
This is the default behaviour _\*\*_that uses a local sqlite file as database. Works great for development and local testing.

```bash
./cloudquery fetch # you can change the default sqlite.db file via --dsn
```
{% endtab %}

{% tab title="MySQL" %}
```bash
./cloudquery fetch --driver mysql --dsn "root:pass@tcp(127.0.0.1:3306)/dbname"
```

To run a local MySQL instance via [docker](https://hub.docker.com/_/mysql):

```bash
docker run -p 3306:3306 -e MYSQL_ROOT_PASSWORD=pass -e MYSQL_DATABASE=dbname -d mysql
```
{% endtab %}

{% tab title="PostgreSQL" %}
```bash
./cloudquery fetch --driver postgresql --dsn "host=localhost user=postgres password=pass DB.name=postgres port=5432"
```

To run a local PostgreSQL instance via [docker](https://hub.docker.com/_/postgres):

```bash
docker run -p 5432:5432 -e POSTGRES_PASSWORD=pass -d postgres
```
{% endtab %}

{% tab title="SQL Server" %}
```bash
./cloudquery fetch --driver sqlserver --dsn "sqlserver://sa:yourStrong(!)Password@localhost:1433?database=cloudquery"
```

To run a local SQL Server instance via [docker](https://hub.docker.com/_/microsoft-mssql-server):

```bash
docker run -it -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=yourStrong(!)Password' -p 1433:1433 mcr.microsoft.com/mssql/server:2019-latest
```
{% endtab %}
{% endtabs %}

## Graph

{% tabs %}
{% tab title="Neo4j" %}
```bash
./cloudquery fetch --driver neo4j --dsn "neo4j://neo4j:pass@localhost:7687"
```

To run a local Neo4j instance via [docker](https://hub.docker.com/_/postgres):

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


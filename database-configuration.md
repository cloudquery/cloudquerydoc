# Database Configuration

cloudquery currently supports two types of databases: **Relational** - PostgreSQL and **graph** - Neo4j.

### Relational

{% tabs %}
{% tab title="PostgreSQL" %}
```bash
./cloudquery fetch --driver postgresql --dsn "host=localhost user=postgres password=pass database=postgres port=5432"
```

To run a local PostgreSQL instance via [docker](https://hub.docker.com/_/postgres):

```bash
docker run -p 5432:5432 -e POSTGRES_PASSWORD=pass -d postgres
```
{% endtab %}

{% tab title="Other" %}
Wanna see support for other database? Please open an [issue](https://github.com/cloudquery/cloudquery/issues):\)
{% endtab %}
{% endtabs %}




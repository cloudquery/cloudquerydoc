# Database Configuration

Cloudquery currently supports only Postgres 11+,  support for Graph and another database engines will be added in the future. 

## Relational

{% tabs %}
{% tab title="PostgreSQL" %}
```bash
./cloudquery fetch --dsn "host=localhost user=postgres password=pass database=postgres port=5432"
```

To run a local PostgreSQL instance via [docker](https://hub.docker.com/_/postgres):

```bash
docker run -p 5432:5432 -e POSTGRES_PASSWORD=pass -d postgres
```
{% endtab %}
{% endtabs %}


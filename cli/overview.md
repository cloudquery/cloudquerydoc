# Overview

The command line interface to Cloudquery is via the `cloudquery` command, which accepts a variety of subcommands such as `cloudquery init` or `cloudquery fetch`. See  full list of all of the supported bellow.

We refer to the `cloudquery` command line tool as "Clouddquery CLI" elsewhere in the documentation.

{% hint style="info" %}
Cloudquery v0.13.0  added support for a console UI in TTY shells. 

If you would like to see everything as logs use the --enable-console-log flag. In both cases logs will be written to your cloudquery.log
{% endhint %}

To view a list of the commands available in your current version, run `cloudquery` with no additional arguments:

```text

CloudQuery CLI

Query your cloud assets & configuration with SQL.
Solve compliance, security and cost challenges with standard SQL queries and relational tables.
Find more information at:
        https://docs.cloudquery.io

Usage:
  cloudquery [command]

Available Commands:
  completion  Generate completion script (run --help for full instructions)
  fetch       Fetch data from configured cloud APIs to specified SQL database
  help        Help about any command
  init        Generate initial config.hcl for fetch command
  policy      Execute a policy on CloudQuery fetched data
  version     Print full version info of cloudquery

Flags:
      --config string               path to configuration file. can be generated with 'gen config' command (env: CQ_CONFIG_PATH) (default "./config.hcl")
      --dsn string                  database connection string (env: CQ_DSN) (example: 'host=localhost user=postgres password=pass DB.name=postgres port=5432')
      --enable-console-log          Enable console logging
      --enable-file-logging         enableFileLogging makes the framework logging to a file (default true)
      --encode-json                 EncodeLogsAsJson makes the logging framework logging JSON instead of KV
  -h, --help                        help for cloudquery
      --log-directory string        Directory to logging to to when file logging is enabled (default ".")
      --log-file string             Filename is the name of the logfile which will be placed inside the directory (default "cloudquery.log")
      --max-age int                 MaxAge the max age in days to keep a logfile (default 3)
      --max-backups int             MaxBackups the max number of rolled files to keep (default 3)
      --max-size int                MaxSize the max size in MB of the logfile before it's rolled (default 30)
      --no-download                 No Download will make hub not download any provider but use existing
      --no-verify                   NoVerify is true registry won't verify the plugins
      --plugin-dir string           Directory to save and load CloudQuery plugins from (env: CQ_PLUGIN_DIR) (default "C:\\Users\\Ron-Work\\Projects\\cloudquery")
      --reattach-providers string   Path to reattach unmanaged plugins, mostly used for testing purposes (env: CQ_REATTACH_PROVIDERS)
  -v, --verbose                     Enable Verbose logging
      --version                     version for cloudquery
```


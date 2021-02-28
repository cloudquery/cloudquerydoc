# Overview

The command line interface to Cloudquery is via the `cloudquery` command, which accepts a variety of subcommands such as `cloudquery init` or `cloudquery fetch`. A full list of all of the supported subcommands is in the navigation section of this page.

We refer to the `cloudquery` command line tool as "Clouddquery CLI" elsewhere in the documentation.

To view a list of the commands available in your current Terraform version, run `cloudquery` with no additional arguments:

```text
cloudquery CLI

Usage:
  cloudquery [command]

Available Commands:
  completion  Generate completion script (run --help for full instructions)
  fetch       Fetch data from configured cloud APIs to specified SQL database
  gen         Generate initial config.yml for fetch command or policy.yml for query command
  help        Help about any command
  init        Initialize CloudQuery by downloading appropriate providers
  query       Run queries specified in a policy file
  version     Print full version info of cloudquery

Flags:
      --enableConsoleLog      Enable console logging (default true)
      --enableFileLogging     enableFileLogging makes the framework logging to a file (default true)
      --encodeLogsAsJson      EncodeLogsAsJson makes the logging framework logging JSON
  -h, --help                  help for cloudquery
      --logDirectory string   Directory to logging to to when file logging is enabled (default ".")
      --logFile string        Filename is the name of the logfile which will be placed inside the directory (default "cloudquery.log")
      --maxAge int            MaxAge the max age in days to keep a logfile (default 3)
      --maxBackups int        MaxBackups the max number of rolled files to keep (default 3)
      --maxSize int           MaxSize the max size in MB of the logfile before it's rolled (default 30)
  -v, --verbose               Enable Verbose logging
      --version               version for cloudquery

Use "cloudquery [command] --help" for more information about a command.
```


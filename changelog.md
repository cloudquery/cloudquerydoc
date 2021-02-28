---
description: "Be sure to not miss out on new features and improvements! \U0001F680"
---

# Changelog

If you have any feedback, don't hesitate to contact us at info@cloudquery.io

## v0.10.0

### Added

*  [db10303](https://github.com/cloudquery/cloudquery/commit/db1030379cc893e3eb1f92acdb54c1e573aaecff) Add examples to fetch --help
* [29bf43a](https://github.com/cloudquery/cloudquery/commit/29bf43a365de3fef62cab6375906d9685613a3f9) Minor config/hub refactor \([\#64](https://github.com/cloudquery/cloudquery/pull/64)\)
* [e63d616](https://github.com/cloudquery/cloudquery/commit/e63d616846f2cbf3b9ca1ac6abd4ecb17ef7085c) Refactor plugin lifecycle management, client and logging \([\#61](https://github.com/cloudquery/cloudquery/pull/61)\)

  ```text
    --enableConsoleLog      Enable console logging (default true)
    --enableFileLogging     enableFileLogging makes the framework logging to a file (default true)
    --encodeLogsAsJson      EncodeLogsAsJson makes the logging framework logging JSON
    --logDirectory string   Directory to logging to to when file logging is enabled (default ".")
    --logFile string        Filename is the name of the logfile which will be placed inside the directory (default "cloudquery.log")
    --maxAge int            MaxAge the max age in days to keep a logfile (default 3)
    --maxBackups int        MaxBackups the max number of rolled files to keep (default 3)
    --maxSize int           MaxSize the max size in MB of the logfile before it's rolled (default 30)
    -v, --verbose           Enable Verbose logging
  ```

### Fixed

*  [d2d7bbd](https://github.com/cloudquery/cloudquery/commit/d2d7bbd28aa75a16183bc27d7d2599c4970c03df) Bugfix panic in cloudquery query


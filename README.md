Log
===

Class Phasty\Log\File provides ability to log into files.

If you have to log many data in production you can meet problems with reading logs soon.

First problem is that usually log file grows fast and it becomes too hard to read such log file
with utilities like less, so navigation over this file becomes unreal.

Second problem is that log rows should have enough information to make decision how to solve your issue.

Current version of logger class allows you to split log files by time as you decide:
by days, by hours or by minutes. Log file changes silently, you should only supply mask for path to file
if default is not what you want. Default is:

    log/%Y/%m/%d/%H/

At 15:00 of 03/10/2014 file will be in log/2014/03/10/15/ directory.
Default file name is "log", so full file path becomes log/2014/03/10/15/log.log .
If you want to divide different type of logged data into different files you can change default
file name at configuration time or at runtime.

Each log line is formatted according to configuration and can include next information automatically in line header:

    Level of logging
    PID of process
    Exact time (microseconds to if needed)
    Used memory

Log message may be spaced from log header by special spacer, default is "+-". For example:

    [D 13762, 20:13.0250, 1048576 ] +-That is debug-level log message
    [E 13762, 20:13.0261, 1048576 ] +-That is error-level log message

Moreover, by default each log line header is highlighted in file according to it's logging level:

![](https://cloud.githubusercontent.com/assets/2020598/3697733/7a448b76-13af-11e4-945f-08f48d5d65fc.png)


USAGE
-----

    use Phasty\Log\File as log;

    log::debug("This is debug message");
    log::info("This is info message");
    log::notice("This is notice message");
    log::success("This is success message");
    log::warning("This is warning message");
    log::error("This is error message");

Configuration
-------------

config/log.php:
    <?php
    return [
        "spacer" => "+-----",
        "header" => [
            "color" => "brown"
        ],
        "name" => "queue"
    ];

using:

    use Phasty\Log\File as log;
    log::config(require "config/log.php");
    log::info("log message");

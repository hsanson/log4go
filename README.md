Fork of http://log4go.googlecode.com/

This is a fork of log4go from [googlecode](http://log4go.googlecode.com/) with
all log rotation part rewritten.

The original version supported daily, maxsize and maxlines file log rotation and
used file names like out.log.001, out.log.002, etc to rename the rotated logs.

The logic to generate those file names caused issues when manipulating the old
logs (e.g. compressing) and resulted in logs being overriden and lost.

The modifications in this fork:

  - Use current date to name rotated filenames (e.g. out.log-2006-01-02)
  - Remove maxsize and maxlines rotation options. Only support daily rotation.

## Installation

    go install github.com/sujrd/log4go

## Usage

To log messages to stdout:

    import l4g "github.com/sujrd/log4go"

    l4g.NewConsoleLogger(l4g.DEBUG)

    l4g.Info("Info message %d", val)
    l4g.Critical("Critical message: %s", err)
    l4g.Debug("Debug message")
    l4g.Error("Error message: %v", err)

To log to a file with daily rotation:

    writer := l4g.NewFileLogWriter("/var/log/out.log", true)
    writer.SetRotate(true)
    l4g.AddFilter("stdout", l4g.ERROR, writer)

    l4g.Info("Info message")

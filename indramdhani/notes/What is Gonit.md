[https://github.com/bitnami/gonit](https://github.com/bitnami/gonit)

Gonit is replacement for Monit

```bash
Usage:
  gonit [flags]
  gonit [command]

Available Commands:
  monitor     Monitor service
  quit        Terminate the execution of a running daemon
  reload      Reinitialize tool
  restart     Restart service
  start       Start service
  status      Print full status information for each service
  stop        Stop service
  summary     Print short status information for each service
  unmonitor   Unmonitor service

Flags:
  -c, --controlfile file        Use this control file (default "/etc/gonit/gonitrc")
  -d, --daemonize n             Run as a daemon once per n seconds
  -I, --foreground              Do not run in background (needed for run from init)
  -l, --logfile file            Print log information to this file. (default "/var/log/gonit.log")
  -p, --pidfile pidfile         Use this pidfile in daemon mode (default "/var/run/gonit.pid")
  -S, --socketfile socketfile   Use this socketfile to listen for requests in daemon mode (default "/var/run/gonit.sock")
  -s, --statefile file          Set the file gonit should write state information to (default "/var/lib/gonit/state")
  -v, --verbose                 Verbose mode, work noisy (diagnostic output)

Use "gonit [command] --help" for more information about a command.
```

#server #gonit #monitoring 
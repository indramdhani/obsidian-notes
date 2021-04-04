# Monit
## Getting Started

[Monit](https://mmonit.com/monit/) is an open source tool for monitoring and active service recovery on Linux. Monit uses control files to determine the action that will be executed based on the server activities.

## Installation

Depend on the system, there are several ways to install monit. You might require sudo access to install monit.

### Building from source code

Download latest monit release from [download area](http://mmonit.com/monit/download/).

Extract and install the source code

```bash
tar zxvf monit-x.y.z.tar.gz (where x.y.z denotes version numbers)
cd monit-x.y.z
./configure (use ./configure --help to view available options)
make && make install
```

### Pre-built binaries

Download pre-built binaries from [download area](https://mmonit.com/monit/#download)

Extract and copy the files to `/etc/`

```bash
tar zxvf monit-x.y.z-linux-x64.tar.gz (x.y.z denotes version numbers)
cd monit-x.y.z
cp bin/monit /usr/local/bin/
cp conf/monitrc /etc/
```

### Install from Software Packages

This is the easiest way to install monit, however on some system the package is not the latest version.

**Ubuntu/Debian**

```bash
aptitude install monit
```

**Fedora**

```bash
yum install monit
```

## Start monit on system boots

### [SystemD](https://mmonit.com/wiki/Monit/Systemd)

Create `monit.service` under `/lib/systemd/system/` directory

```bash
cd /lib/systemd/system/

touch monit.service
#or
nano monit.service
```

Copy the script below to `monit.service`

```bash
# This file is systemd template for monit service. To
 # register monit with systemd, place the monit.service file
 # to the /lib/systemd/system/ directory and then start it
 # using systemctl (see below).
 #
 # Enable monit to start on boot: 
 #         systemctl enable monit.service
 #
 # Start monit immediately: 
 #         systemctl start monit.service
 #
 # Stop monit:
 #         systemctl stop monit.service
 #
 # Status:
 #         systemctl status monit.service

 [Unit]
 Description=Pro-active monitoring utility for unix systems
 After=network-online.target
 Documentation=man:monit(1) <https://mmonit.com/wiki/Monit/HowTo> 

 [Service]
 Type=simple
 KillMode=process
 ExecStart=/usr/local/bin/monit -I
 ExecStop=/usr/local/bin/monit quit
 ExecReload=/usr/local/bin/monit reload
 Restart = on-abnormal
 StandardOutput=null

 [Install]
 WantedBy=multi-user.target
```

### [Upstart](https://mmonit.com/wiki/Monit/Upstart)

Create `monit.conf` under `/etc/init`

```bash
cd /etc/init/

touch monit.conf
#or 
nano monit.conf
```

Copy the script below to the `monit.conf`

```bash
# This is an upstart script to keep monit running.
 # To install disable the old way of doing things:
 #
 #   /etc/init.d/monit stop && update-rc.d -f monit remove
 #
 # then put this script here:
 #
 #   /etc/init/monit.conf
 #
 # and reload upstart configuration:
 #
 #   initctl reload-configuration
 #
 # You can manually start and stop monit like this:
 # 
 # start monit
 # stop monit
 #

 description "Monit service manager"

 limit core unlimited unlimited

 start on runlevel [2345]
 stop on starting rc RUNLEVEL=[016]

 expect daemon
 respawn

 exec /usr/local/bin/monit -c /etc/monitrc

 pre-stop exec /usr/local/bin/monit -c /etc/monitrc quit
```

# Basic Usage

The binary file is located in `/usr/local/bin/monit`.

The basic configuration is located in `/etc/monitrc`. While the additional configuration is located in `/etc/monit.d/`.

The log file can be found in `/var/log/monit.log`.

## Basic Configuration

Let's start configuring monit. All the configuration below is located in `/etc/monitrc`

```bash
nano /etc/monitrc
```

### Update the monitoring intervals

```bash
...
###############################################################################
## Global section
###############################################################################
##
## Start Monit in the background (run as a daemon):
#
set daemon  *secondsInterval*              # check services at 30 seconds intervals
   with start delay *secondDelay*    # optional: delay the first check by 4-minutes (by
#                           # default Monit check immediately after Monit start)
...
```

Replace the _secondsInterval_ and _secondDelay_ with number in seconds

### Update the mailserver

```bash
...
## Set the list of mail servers for alert delivery. Multiple servers may be
## specified using a comma separator. If the first mail server fails, Monit
# will use the second mail server in the list and so on. By default Monit uses
# port 25 - it is possible to override this with the PORT option.
#
set mailserver *primaryMailServer*  port *mailServerPort* username *mailServerUsername* password *mailServerPassword* using TLSV1,  
# set mailserver mail.bar.baz,               # primary mailserver
#                backup.bar.baz port 10025,  # backup mailserver on port 10025
#                localhost                   # fallback relay
#
...
```

Replace the _primaryMailServer, mailServerPort, mailServerUsername_ and _mailServerPassword_

### Setup alert recipient

```bash
...
## You can set alert recipients whom will receive alerts if/when a
## service defined in this file has errors. Alerts may be restricted on
## events by using a filter as in the second example below.
#
# set alert sysadm@foo.bar                       # receive all alerts
# set alert indra@krafthaus.id
## Do not alert when Monit starts, stops or performs a user initiated action.
## This filter is recommended to avoid getting alerts for trivial cases.
#
# set alert your-name@your.domain not on { instance, action }
...
```

### Setup the Monit HTTP interface

```bash
..
set httpd port 2812 and 
    allow 52.221.104.21
    allow localhost        # allow localhost to connect to the server and
    allow admin:monit   # require user 'admin' with password 'monit'
    with ssl {            # enable SSL/TLS and set path to server certificate
         pemchain: /etc/letsencrypt/cert.pem
         pemkey: /etc/letsencrypt/privkey.pem
         selfsigned: allow
    }
...
```

As default, Monit can be accesible via port 2812

To setup the authentication use `allow` keyword. It can be the allowed ip address or allowed user and password

If you are going to use https, please setup the `with ssl` block with the respective server certificate

### [Monit basic argument](https://mmonit.com/monit/documentation/monit.html#Arguments)

Monit has several argument, that used to control monit

**Start monit for the first time**

```bash
sudo /usr/local/bin/monit
```

**Quit monit**

```bash
sudo /usr/local/bin/monit quit
```

**Validate the monit configuration**

```bash
sudo /usr/local/bin/monit -t
```

**Reload the monit configuration**

```bash
sudo /usr/local/bin/monit reload
```

You can find another argument [here](https://mmonit.com/monit/documentation/monit.html#Arguments)

## Adding service check

As a default, there are several examples of service check located on `/etc/monitrc`. Let's add another monitoring rule under `/etc/monit.d`.

Service check structure as below

```bash
CHECK 
SERVICE TYPE #[PROCESS|FILE|FIFO|FILESYSTEM|DIRECTORY|HOST|SYSTEM|PROGRAM|NETWORK] 
uniqueName  
[WITH PIDFILE|WITH PATH|ADDRESS] [pathToFile|Address]
	SERVICE GROUP #optional, used to group the service check
	SERVICE METHOD # consist of Start, stop and restart
	SERVICE TEST # list of test that can be applied to service type
```

Below are several example service check

```bash
check host mmonit.com with address mmonit.com
      if failed port 80 protocol http then alert
      if failed port 443 protocol https then alert
```

```bash
check host mmonit.com with address mmonit.com
      if failed
         port 80 protocol http
         and status = 200
         and request /monit/ with content = "Monit [0-9.]+"
      then alert
```

```bash
check host smtp.example.com with address smtp.example.com
      if failed port 25 with protocol smtp then alert

check host localhost with address 127.0.0.1
      if failed ping then alert        
      if failed port 3306 protocol mysql then alert
```

```bash
check host mmonit.com with address mmonit.com
      if failed
         port 443
         with protocol https
         and certificate valid > 30 days
         use ssl options {verify: enable}
      then alert
```

```bash
check process apache with pidfile /var/run/httpd.pid
      start program = "/etc/init.d/apache2 start"
      stop  program = "/etc/init.d/apache2 stop"
			restart program  = "/etc/init.d/apache2 restart"
      if failed port 80 protocol http then restart
			# or if failed port 80 protocol http for 2 cycles then restart
			# check the resource
      if cpu > 95% for 2 cycles then alert
      if total cpu > 99% for 10 cycles then restart
      if memory > 50 MB then alert
      if total memory > 500 MB then restart
      if disk read > 10 MB/s for 2 cycles then alert
```

```bash
check file access.log with path /var/log/apache2/access_log
      if size > 250 MB then exec "/usr/sbin/logrotate -f apache"
      if failed checksum then alert 
      if failed uid root then alert
      if failed gid root then alert
      if failed permission 755 then alert
```

```bash
check directory certificates with path /etc/ssl/certs/
      if changed timestamp then alert
			#or if timestamp > 1 hour then alert
```

```bash
check filesystem disk2 with path /dev/disk2
      if space usage > 95% then alert
      if service time > 300 milliseconds for 5 cycles then alert
```

Find the complete reference [here](https://mmonit.com/monit/documentation/monit.html)

# References

[](https://mmonit.com/wiki/)[https://mmonit.com/wiki/](https://mmonit.com/wiki/)

[](https://mmonit.com/monit/documentation/monit.html)[https://mmonit.com/monit/documentation/monit.html](https://mmonit.com/monit/documentation/monit.html)

#server #monitoring #monit
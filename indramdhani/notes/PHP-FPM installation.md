# PHP-FPM Installation
Depend on the os image, there are 2 ways to configure php-fpm

## AWS

### Install the needed version

```bash
#find the needed php-fpm version
sudo yum search php-fpm
#install the needed php-fpm version
sudo yum install php73-fpm php72-fpm ...
```

### Update the configuration to use different port

The configuration is available at `www.conf` usually the file is under `/etc/php-fpm-7.3.d/`

```bash
sudo nano /etc/php-fpm-7.3.d/www.conf
```

update the line below

```bash
...
; RPM: apache user chosen to provide access to the same directories as httpd
user = apache
; RPM: Keep a group allowed to write in log dir.
group = www
...
listen = 127.0.0.1:9000
...
pm = dynamic
...
pm.max_children = 25
...
pm.start_servers = 8
...
pm.min_spare_servers = 4
...
pm.max_spare_servers = 12
... 
;pm.status_path = /status
... 
;ping.response = pong
...
request_slowlog_timeout = 180s
...
```

to be

```bash
...
; RPM: apache user chosen to provide access to the same directories as httpd
user = ec2-user
; RPM: Keep a group allowed to write in log dir.
group = www
...
listen = 127.0.0.1:9073
...
pm = ondemand
...
pm.max_children = 25
...
pm.start_servers = 8
...
pm.min_spare_servers = 4
...
pm.max_spare_servers = 12
... 
pm.status_path = /73-status
... 
ping.response = pong
...
request_slowlog_timeout = 180s
...
```

### Update the init.d to use different configuration

The configuration file located in `/etc/init.d` the file name format usually is `php-fpm-7.3`. The init.d configuration needs to be updated to make sure each service use different php-fpm configuration

```bash
sudo nano /etc/init.d/php-fpm-7.3
```

Update the line below

```bash
start () {
        echo -n $"Starting $prog: "
        dir=$(dirname ${pidfile})
        [ -d $dir ] || mkdir $dir
        daemon --pidfile ${pidfile} /usr/sbin/php-fpm-7.3 --daemonize $OPTIONS
        RETVAL=$?
        echo
        [ $RETVAL -eq 0 ] && touch ${lockfile}
}
```

to be

```bash
start () {
        echo -n $"Starting $prog: "
        dir=$(dirname ${pidfile})
        [ -d $dir ] || mkdir $dir
        daemon --pidfile ${pidfile} /usr/sbin/php-fpm-7.3 -y /etc/php-fpm-7.3.conf --daemonize $OPTIONS
        RETVAL=$?
        echo
        [ $RETVAL -eq 0 ] && touch ${lockfile}
}
```

## Remirepo

Follow the wizard [here](https://rpms.remirepo.net/wizard/) then update the php-fpm configuration to use different port.

The configuration file is located in `/etc/opt/remi/php74/php-fpm.d/` the file name is `www.conf`

## Setup Status Page

To enable status page, add new configuration file in the httpd directory.

Let's create `server-status.conf` in `/ect/httpd/conf.modules.d`

```bash
cd /etc/httpd/conf.modules.d/
sudo nano server-status.conf
```

Add the block below

```bash
<Location "/73-status">
		SetHandler "proxy:fcgi://127.0.0.1:9073"      
</Location>

<Location "/73-ping">
		SetHandler "proxy:fcgi://127.0.0.1:9073"
</Location>
```

Add block below to block unauthorized access. The status page will be accessible for the IP address listed

```bash
...
Require ip 127.0.0.1
Require ip 52.221.104.21
...
```

The final block

```bash
<Location "/73-status">
  SetHandler "proxy:fcgi://127.0.0.1:9073"
  Require ip 52.221.104.21
</Location>

<Location "/73-ping">
  SetHandler "proxy:fcgi://127.0.0.1:9073"
  Require ip 52.221.104.21
</Location>
```

#server #php
## Installation

Depend on the OS, there are 2 httpd source that can be used ( or use httpd version that supports h2 )

### AWS

```bash
sudo yum install httpd
```

### Codeit

```bash
sudo yum install epel-release
```

```bash
cd /etc/yum.repos.d && wget <https://repo.codeit.guru/codeit.el`rpm> -q --qf "%{VERSION}" $(rpm -q --whatprovides redhat-release)`.repo
```

```bash
yum install httpd
```

## Post-installation

## Enable on startup

To enable the service on server boot run command below

```bash
sudo systemctl enable httpd
#or
sudo service httpd enable
#or
sudo chkconfig httpd on
```

### Setup apache worker

The configuration is located in different location depending on the system / OS used. Usually it will be under `/etc/httpd/conf.modules.d` directory. Edit the `00-mpm.conf` comment the mpm\_prefork and remove the comment sign from mpm\_worker or mpm\_event. The mpm\_worker or mpm\_event is needed in order to enable HTTP2 / H2

```bash
# Select the MPM module which should be used by uncommenting exactly
# one of the following LoadModule lines.

# prefork MPM: Implements a non-threaded, pre-forking web server
# See: <http://httpd.apache.org/docs/2.4/mod/prefork.html>
#
# NOTE: If enabling prefork, the httpd_graceful_shutdown SELinux
# boolean should be enabled, to allow graceful stop/shutdown.
#
#LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

# worker MPM: Multi-Processing Module implementing a hybrid
# multi-threaded multi-process web server
# See: <http://httpd.apache.org/docs/2.4/mod/worker.html>
#
LoadModule mpm_worker_module modules/mod_mpm_worker.so

# event MPM: A variant of the worker MPM with the goal of consuming
# threads only for connections with active processing
# See: <http://httpd.apache.org/docs/2.4/mod/event.html>
#
#LoadModule mpm_event_module modules/mod_mpm_event.so
```

## Setup vhost / proxy reserve

To set up the additional vhost we need to add one block of the vhost script to httpd configuration. To make it easier to manage, we can create one directory that will be used to put all vhost configuration.

```bash
#move to httpd directory
cd /etc/httpd
# create new directory
sudo mkdir conf.vhost.d
```

Include the `conf.vhost.d` into httpd configuration by editing this file `/etc/httpd/conf/httpd.conf` and add the line below

```bash
...
IncludeOptional conf.vhost.d/*.conf
```

Under `/etc/httpd/conf.vhost.d` we can put a vhost file that contains

```bash
<Virtualhost *:80> 
  ServerName server.name
  ServerAlias www.server.name
  DocumentRoot /path/to/app/directory
  <Directory /path/to/app/directory/>
    <FilesMatch \\.php$>
       SetHandler "proxy:fcgi://127.0.0.1:9072"
    </FilesMatch>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
  </Directory>
</Virtualhost>
```

Proxy reserve configuration example

```bash
#  SSLEngine on
#  SSLProxyEngine on
SSLProxyVerify none
SSLProxyCheckPeerCN off
SSLProxyCheckPeerName off
SSLProxyCheckPeerExpire off 

ProxyPass "/api/design/"<http://127.0.0.1:7080/>
ProxyPassReverse "/api/design/"<http://127.0.0.1:7080/>

ProxyPass "/api/mysql"<http://127.0.0.1:7174/>
ProxyPassReverse "/api/mysql" <http://127.0.0.1:7174/>

ProxyPass "/api/mongo" <http://127.0.0.1:7274/>
ProxyPassReverse "/api/mongo" <http://127.0.0.1:7274/>

ProxyPass "/api/csp/" <http://127.0.0.1:7076/>
ProxyPassReverse "/api/csp/" <http://127.0.0.1:7076/>

```

## Setup https / ssl

If we are going to setup the https version, we can add the block below

```bash
<VirtualHost *:443>
  Protocols h2 h2c http/1.1
  Header always set Strict-Transport-Security "max-age=63072000; includeSubdomains; preload"

  ServerName server.name:443
  ServerAlias www.server.name:443        

  ErrorLog logs/ssl_error_log
  LogLevel warn

  SSLEngine on
  SSLProtocol all  -SSLv3 -TLSv1 -TLSv1.1

  SSLCipherSuite "EECDH+ECDSA+AESGCM EECDH+aRSA+AESGCM EECDH+ECDSA+SHA384 EECDH+ECDSA+SHA256 EECDH+aRSA+SHA384 EECDH+aRSA+SHA256 EECDH+aRSA+RC4 EECDH EDH+aRSA RC4 !aNULL !eNULL !LOW !3DES !M$"
  #SSLCipherSuite          ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384
  SSLHonorCipherOrder off
  SSLCompression      off
  SSLSessionTickets       off
  ServerAlias dev.paperlust.co
  SSLCertificateFile /etc/letsencrypt/live/www.dev.paperlust.co/fullchain.pem
  SSLCertificateKeyFile /etc/letsencrypt/live/www.dev.paperlust.co/privkey.pem
  SSLCACertificateFile /media/site_data/certs/paperlust-bundle.crt

  <Files ~ "\\.(cgi|shtml|phtml|php3?)$">
    SSLOptions +StdEnvVars
  </Files>
  <Directory "/var/www/cgi-bin">
     SSLOptions +StdEnvVars
  </Directory>
        BrowserMatch "MSIE [2-5]"nokeepalive ssl-unclean-shutdown downgrade-1.0 force-response-1.0

CustomLog logs/ssl_request_log "%h %l %u %t \\"%r\\" %>s %b \\"%{Referer}i\\" \\"%{User-Agent}i\\" %{SSL_PROTOCOL}x %{SSL_CIPHER}x"

DocumentRoot "/media/site_data/dev/html"
  <Directory "/media/site_data/dev/html">
    Require all granted
    AllowOverride all
    <FilesMatch \\.php>
      SetHandler "proxy:fcgi://127.0.0.1:9072"
    </FilesMatch>
  </Directory>
</VirtualHost>
```

### Enable HTTP2 / H2

The requirement of H2 are

-   The HTTPS have to be enabled, with TLS protocol version ≥ 1.2.
    
-   The minimum version of HTTPD is Apache 2.4.17 or above.
    
-   Disable the mod\_php and replace it with php-fpm module. You can find it on [PHP-FPM Installation](https://www.notion.so/PHP-FPM-Installation-f0185634638d4d0fb3c0b63d6bb07eaa)
    
-   Change the mpm\_prefork with mpm\_event or mpm\_worker.
    
-   Load the mod\_http2 module. The configuration is located in different location depending on the system / OS used. Usually it will be under `/etc/httpd/conf.modules.d` directory. Edit the `00-base.conf` and remove the comment from mod\_httpd2
    
    ```bash
    ...
    LoadModule http2_module modules/mod_http2.so
    ...
    ```
    
-   Enable H2 by adding following line into global configuration or inside of particular virtual host
    
    ```bash
    Protocols h2 http/1.1
    ```
    
-   Reload or restart the httpd
    
    ```bash
    #check the http config file first before restart / reload the service
    sudo httpd -t
    
    sudo service httpd restart
    # or
    sudo service httpd reload
    or
    sudo systemctl restart httpd
    ```
    

### Setup status page

To enable status page, add new configuration file in the httpd directory.

Let's create `server-status.conf` in `/ect/httpd/conf.modules.d`

```bash
cd /etc/httpd/conf.modules.d/
sudo nano server-status.conf
```

Add the block below

```bash
ExtendedStatus On

<Location "/server-status">
    SetHandler server-status
</Location>
```

Add block below to block unauthorized access. The status page will be accessible for the IP address listed

```bash
...
Require ip 49.128.176.154
Require ip 127.0.0.1
Require ip 52.64.192.203
Require ip 52.86.21.59
Require ip 52.221.104.21
Require ip 54.179.44.207
...
```

The final block

```bash
ExtendedStatus On

<Location "/server-status">
		SetHandler server-status
		Require ip 49.128.176.154
		Require ip 127.0.0.1
		Require ip 52.64.192.203
		Require ip 52.86.21.59
		Require ip 52.221.104.21
		Require ip 54.179.44.207
</Location>
```

#server #httpd
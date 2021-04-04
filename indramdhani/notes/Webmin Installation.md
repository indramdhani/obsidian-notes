### Via RPM

```bash
wget <http://prdownloads.sourceforge.net/webadmin/webmin-1.972-1.noarch.rpm>
```

```bash
yum -y install perl perl-Net-SSLeay openssl perl-IO-Tty perl-Encode-Detect
```

```bash
rpm -U webmin-1.972-1.noarch.rpm
```

### Via Yum Repo

```bash
[Webmin]
name=Webmin Distribution Neutral
#baseurl=https://download.webmin.com/download/yum
mirrorlist=https://download.webmin.com/download/yum/mirrorlist
enabled=1
```

```bash
wget <https://download.webmin.com/jcameron-key.asc>
rpm --import jcameron-key.asc
```

```bash
yum install webmin
```

### Change the port

To change the webmin port edit the `/etc/webmin/miniserv.conf`

```bash
sudo nano /etc/webmin/miniserv.conf
```

and change the line below

```bash
port=10000
...
```

update it to be

```bash
port=8541
...
```

restart the webmin

```bash
sudo service webmin restart
#or
sudo systemctl restart webmin
#or 
sudo /etc/init.d/webmin restart
```

### Change password

```bash
sudo /usr/libexec/webmin/changepass.pl /etc/webmin user newpassword
```

#server #management #webmin
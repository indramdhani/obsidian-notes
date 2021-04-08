# CXS Installation
## Product Requirements:

-   Cpanel/WHM
-   InterWorx
-   DirectAdmin
-   Plesk Onyx/Obsidian
-   VestaCP
-   CentOS web panel
-   CyberPanel
-   Server with static IP
-   Redhat/CentOS/Cloudlinux
-   ClamAV
-   SQLite v3
-   ModSecurity
-   Kernel with inotify support

## Prerequisites Installation:

### RPM Modules:

#### RedHat related OS's:

The EPEL repository will likely need to be used to install all of the required perl rpms. Choose the one appropriate to your OS:

```bash
# yum install <https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm>
# yum install <https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm>
# yum install <https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm>
yum config-manager --set-enabled PowerTools
```

After installing the epel-release, clean the yum cache with

```bash
yum clean all
```

```bash
yum install perl-libwww-perl.noarch perl-LWP-Protocol-https.noarch perl-Archive-Tar.noarch perl-Archive-Zip.noarch perl-Linux-Inotify2 perl-Compress-Zlib sqlite perl-DBI perl-DBD-SQLite perl-IO-Socket-SSL.noarch perl-Net-SSLeay.x86_64 sqlite
```

#### For Debian related OS's:

```bash
apt-get install libcompress-raw-zlib-perl libarchive-tar-wrapper-perl libarchive-zip-perl libwww-perl liblwp-protocol-https-perl liblinux-inotify2-perl libcgi-pm-perl sqlite3 libdbi-perl libdbd-sqlite3-perl
```

## ClamAV Installation:

For RedHat related OS's we recommend using the epel repository:

[](https://fedoraproject.org/wiki/EPEL)[https://fedoraproject.org/wiki/EPEL](https://fedoraproject.org/wiki/EPEL)

 NOTE: clamd needs to run as root, e.g. in /etc/clamd.conf or

```bash
# /etc/clam.d/scan.conf and the local socket option enabled
```

```bash
yum -y install clamav-server clamav-data clamav-update clamav-filesystem clamav clamav-scanner-systemd clamav-devel clamav-lib clamav-server-systemd
```

```bash
sed -i -e "s/^Example/#Example/" /etc/clamd.d/scan.conf
```

```bash
sed -i -e "s/^Example/#Example/" /etc/freshclam.conf
```

Now edit /etc/clamd.d/scan.conf and change:

```bash
#LocalSocket /var/run/clamd.scan/clamd.sock
...
User clamscan
```

to:

```bash
LocalSocket /var/run/clamd.scan/clamd.sock
...
User root
```

Now update, start and enable clamd:

```bash
freshclam
systemctl start clamd@scan
systemctl enable clamd@scan
```

You will then need to wait until clamd has fully started and created the socket at:

```bash
ls -la /var/run/clamd.scan/clamd.sock
```

## CXS Installation:

```bash
cd /usr/src
rm -f cxs*
wget <https://download.configserver.com/cxsinstaller.tgz>
tar -xzf cxsinstaller.tgz
perl cxsinstaller.pl ipv4
rm -fv cxsinstaller.*
```

## Webmin Module Installation:

-   Install cxs as above
-   Install the cxs webmin module in:
    -   Webmin > Webmin Configuration > Webmin Modules > From local file > /etc/cxs/cxswebmin.tgz > Install Module

#server #cxs #security
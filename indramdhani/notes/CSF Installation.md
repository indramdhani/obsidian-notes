### Installation

```bash
cd /usr/src
rm -fv csf.tgz
wget <https://download.configserver.com/csf.tgz>
tar -xzf csf.tgz
cd csf
sh install.sh
```

## Post Installation

```bash
perl /usr/local/csf/bin/csftest.pl
```

```bash
sh /usr/local/csf/bin/remove_apf_bfd.sh
```

```bash
yum install perl-libwww-perl.noarch perl-LWP-Protocol-https.noarch perl-GDGraph
```

## Webmin Modules

-   Install csf as above
-   Install the csf webmin module in:

```bash
Webmin > Webmin Configuration > Webmin Modules >
  From local file > /usr/local/csf/csfwebmin.tgz > Install Module
```

#server #security #csf
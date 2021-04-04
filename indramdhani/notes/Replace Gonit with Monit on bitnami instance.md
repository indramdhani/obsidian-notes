turn off the gonit

`sudo service gonit stop`

install monit

`sudo apt install monit`

if needed copy gonit configuration to monit folder

`sudo cp /opt/bitnami/config/monit/conf.d/* /etc/monit/conf.d`

configure monitrc as needed

`/etc/monit.d/monitrc`

check the configuration file

`sudo monit -t`

start monit

```bash
sudo service monit start
monit
monit monitor all
```

---

[https://community.bitnami.com/t/monit-server-not-starting-on-port-2812/58779/3](https://community.bitnami.com/t/monit-server-not-starting-on-port-2812/58779/3)

[https://docs.bitnami.com/general/infrastructure/lamp/administration/configure-use-gonit/](https://docs.bitnami.com/general/infrastructure/lamp/administration/configure-use-gonit/)

#server #monitoring #gonit
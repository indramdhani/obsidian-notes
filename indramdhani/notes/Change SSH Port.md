# Change SSH port 

## Notes

By default SSH is using port 22. We can change it to be another port to make it more secure.

Open terminal and connect to your server using SSH

### Find sshd\_config and open it in editor

```bash
sudo nano /etc/ssh/sshd_config
```

### Set the new port

Find line below:

```bash
#Port 22
```

Remove the comment mark and change the port number

```bash
Port 2222
```

Save the file.

### (optional) Update the SELinux rule & Firewall

```bash
semanage port -a -t ssh_port_t -p tcp 2222
```

If you use firewall, please open port 2222

### Restart the ssh service

```bash
sudo service sshd restart
```

or

```bash
sudo systemctl restart sshd
```

### Test the new port

Before closing the current ssh connection, let's test the new port by opening new ssh session with new port. If it succeeded, it means the port changing is success.

#server #ssh #security
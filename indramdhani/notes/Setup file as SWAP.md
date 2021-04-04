Use dd command to create a swap file on the root file system. bs is the block size and count is the number of block size

```bash
sudo dd if=/dev/zero of=/swapfile bs=128M count=32
```

Update the read-write permission for the swap file

```bash
sudo chmod 600 /swapfile
```

Set up a linux swap area

```bash
sudo mkswap /swapfile
```

Enable swap file immediately

```bash
sudo swapon /swapfile
```

Verify the swap file

```bash
sudo swapon -s
```

Enable swap on boot time by editing `/etc/fstab`

```bash
sudo vi /etc/fstab
# or
sudo nano /etc/fstab
```

Add the line below to fstab

```bash
/swapfile swap swap defaults 0 0
```

#server #swap #performance
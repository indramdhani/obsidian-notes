Login in to the instance using SSH

List the available volumes:

```bash
sudo fdisk -l
```

Select a device to partition from the list, let's use /dev/xvda.

```bash
sudo fdisk /dev/xvda
```

Create a new partition

```bash
-> n
```

Select a partition type, let's use primary

```bash
-> p
```

Assign the partition number, let's use partition 2:

```bash
-> 2
```

Accept the default of "First sector" by pressing **Enter.**

Enter the size of the swap file, let's use 4GB of swap file

```bash
-> +4G
```

Save and exit

```bash
-> w
```

### Setup the swap area

Use `partprobe` command to inform the OS of partition table change:

```bash
partprobe
```

Setup a linux swap area using the swap partition, let's use `/dev/xvda1`.

```bash
mkswap /dev/xvda1
```

Add the partition as swap space

```bash
sudo swapon /dev/xvda2
```

Show the current swap space

```bash
sudo swapon -s
```

### Update fstab to make the swap allocation permanent on reboot

Update the `/etc/fstab`, add new entry to make the swap partition available on reboot

```bash
sudo nano /etc/fstab
```

Add the new entry

```bash
/dev/xvda1 none swap sw 0 0
```

#server #swap #performance 
Navigating around

```bash
ls
ls -a
ls -alh
```

```bash
cd 
cd /path/to/go
cd ..
pwd
```

Files and Directories ( create, delete, move, copy, archive )

```bash
mkdir directoryname

rm directoryname 
rm filename
rm -rf directoryname

cp file.extension /path/to/go/
cp oldname.extension newname.extension
cp -R directory /path/to/go/

mv file.extension /path/to/go/
mv oldname.extension newname.extension

tar -czvf folder.tar.gz folder
tar -xzvf folder.tar.gz

zip -r folder.zip folder -r
unzip folder.zip
```

Files and Directories ( ownership, permissions )

```bash
chown -R user:group file 
chmod -R 755 /path/to/file/*
chmod +x /path/to/file.extension

find /path/to/dir -type d -exec chmod 755 {} \\;
find /path/to/dir -type f -exec chmod 644 {} \\;
```

file / folder permission

```
U G W ( User Group World ) 
r = read -> 4
w = write -> 2
x = execute -> 1
- = no access 0 

user with full access will be rwx or 7 ( 4 + 2 + 1 )
group with read-execute access will be r-x - or 5 ( 4 + 1 )
world with read-write access will be rw or 6 ( 4 + 2 )
```

Files ( searching )

```bash
grep string
grep -r "string to find"
find /path/to/find -type f -name "filename"
find /path/to/find -type f -ctime -7
find /path/to/find -type f "*.extension*" -ctime -7
ls | grep string
```

File reading

```bash
cat /file/to/read

tail -n 100 /file/to/read
tail -f /file/to/read
```

File editing

```bash
nano /file/to/edit
vi /file/to/edit
vim /file/to/edit
```

File transfer

```bash
wget <https://external.file/to.download>
curl -0 <https://external.file/to.download>
```

Disk, usage & space

```bash
df -h
du --max-depth=1 -h
du -sh *

lsblk
blkid

sudo du -a /path/to/check/ | sort -n -r | head -n 20

mount
unmount
```

Port

```bash
sudo lsof -i -P -n | grep LISTEN
sudo netstat -ntulap
```

Check process or memory

```bash
free -h
vmstat 1
ps aux 

htop
top

sudo smem -tp
```

Kill Process

```bash
pkill processid
```

Network

```bash
dig
whois 
host
ping
hostname
```

Install

```bash
yum install packagename
yum search packagename
yum info packagename
yum update
yum remove package

rpm -i /path/to/package.rpm

tar zxvf sourcecode.tar.gz
cd sourcecode
./configure
make && make install
```

Service

```bash
service servicename status
service servicename start
service servicename stop
service servicename restart
service servicename reload
```

---

### References

[](https://www.linuxtrainingacademy.com/linux-commands-cheat-sheet/)[https://www.linuxtrainingacademy.com/linux-commands-cheat-sheet/](https://www.linuxtrainingacademy.com/linux-commands-cheat-sheet/)

[](https://wpjohnny.com/linux-server-commands-cheatsheet/)[https://wpjohnny.com/linux-server-commands-cheatsheet/](https://wpjohnny.com/linux-server-commands-cheatsheet/)

[](https://www.rapidtables.com/code/linux/mv.html)[https://www.rapidtables.com/code/linux/mv.html](https://www.rapidtables.com/code/linux/mv.html)

[](https://linuxize.com/post/how-to-copy-files-and-directories-in-linux/)[https://linuxize.com/post/how-to-copy-files-and-directories-in-linux/](https://linuxize.com/post/how-to-copy-files-and-directories-in-linux/)

[](https://geekflare.com/cheat-sheet-system-admin/)[https://geekflare.com/cheat-sheet-system-admin/](https://geekflare.com/cheat-sheet-system-admin/)

#server #bash #shell
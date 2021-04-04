# Database Installation
Depends on which version that need to be installed.

## Mariadb 5.5

```bash
sudo yum install mariadb-server
```

## Latest Mariadb

```bash
sudo yum install wget
wget <https://downloads.mariadb.com/Mariadb/mariadb_repo_setup>
chmod +x mariadb_repo_setup
sudo ./mariadb_repo_setup
```

```bash
sudo yum install mariadb-server
```

## Post Installation

Enable mariadb on boot and start the mariadb

```bash
#enable mariadb on boot
sudo systemctl enable mariadb
or

#start mariadb
sudo systemctl start mariadb
```

Secure mysql installation

```bash
sudo mysql_secure_installation
```

## Setup [PHPMyAdmin](https://docs.phpmyadmin.net/en/latest/setup.html)

1.  Choose an appropriate distribution kit from the [phpmyadmin.net](http://phpmyadmin.net) Downloads page. Some kits contain only the English messages, others contain all languages. We’ll assume you chose a kit whose name looks like `phpMyAdmin-x.x.x -all-languages.tar.gz`.
2.  Ensure you have downloaded a genuine archive, see [Verifying phpMyAdmin releases](https://docs.phpmyadmin.net/en/latest/setup.html#verify).
3.  Untar or unzip the distribution (be sure to unzip the subdirectories): `tar -xzvf phpMyAdmin_x.x.x-all-languages.tar.gz` in your webserver’s document root. If you don’t have direct access to your document root, put the files in a directory on your local machine, and, after step 4, transfer the directory on your web server using, for example, FTP.
4.  Ensure that all the scripts have the appropriate owner (if PHP is running in safe mode, having some scripts with an owner different from the owner of other scripts will be a problem). See [4.2 What’s the preferred way of making phpMyAdmin secure against evil access?](https://docs.phpmyadmin.net/en/latest/faq.html#faq4-2) and [1.26 I just installed phpMyAdmin in my document root of IIS but I get the error “No input file specified” when trying to run phpMyAdmin.](https://docs.phpmyadmin.net/en/latest/faq.html#faq1-26) for suggestions.
5.  Now you must configure your installation. There are two methods that can be used. Traditionally, users have hand-edited a copy of `config.inc.php`, but now a wizard-style setup script is provided for those who prefer a graphical installation. Creating a `config.inc.php` is still a quick way to get started and needed for some advanced features.


#database #server #mariadb
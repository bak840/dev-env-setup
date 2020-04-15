# WSL Setup

## Install WSL

1. Open PowerShell as Administrator and run:  

    ```bash
    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
    ```

2. Restart your computer when prompted

3. Open the Microsoft Store and download Ubuntu

4. Open Ubuntu in the Start menu, set up a new account and run :  

    ```bash
    sudo apt update && sudo apt upgrade
    ```

## WSL setup VS Code

[Developing in WSL](https://code.visualstudio.com/docs/remote/wsl)

## Install Node

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
```

```bash
command -v nvm
```

```bash
nvm ls
```

```bash
nvm install node --lts
```

```bash
node --version
npm --version
```

## Install LAMP server

1. Install packages0010

```bash
sudo apt install apache2 php libapache2-mod-php mariadb-server php-mysql
```

1. Install additional PHP tools

```bash
sudo apt install php-curl php-gd php-intl php-json php-mbstring php-xml php-zip
```

## Configure LAMP server

### Configure Apache server

1. Create project folder

```bash
sudo mkdir /mnt/c/Users/bakou/Workspace/server
```

1. Create symbolic link to the selected folder

```bash
sudo ln -s /mnt/c/Users/bakou/Workspace/server /var/www/devroot
```

1. Open the Apache default virtual host configuration file:

```bash
sudo nano /etc/apache2/sites-enabled/000-default.conf
```

1. Modify the document root to “/var/www/devroot”, which points to your project folder outside of WSL’s filesystem. Set ServerName to localhost (if the port 80 is reserved by a Windows application, replace 80 with an unused port):

```bash
<VirtualHost *:80>        ServerName localhost        ServerAdmin webmaster@localhost        DocumentRoot  /var/www/devroot      <Directory /var/www/>        Options Indexes FollowSymLinks        AllowOverride All        Require all granted      </Directory>        ErrorLog ${APACHE_LOG_DIR}/error.log        CustomLog ${APACHE_LOG_DIR}/access.log combined</VirtualHost>
```

When you are finished, save the file by pressing Ctrl-O, and hit Enter to confirm. Exit with Ctrl-X.

1. Open your favorite Windows editor/IDE, and create an “index.html” file in your project folder (C:\Users\bakou\Workspace\server) with the following content:

```bash
<!DOCTYPE html><html lang="en"><head>  <meta charset="utf-8">  <title>It works!</title></head>&lt;body>  <h1>It works!</h1></body></html>
```

1. Start/Stop the Apache HTTP server:

```bash
sudo service apache2 start
sudo service apache2 stop
```

1. Enable/Disable auto start:

```bash
sudo systemctl enable apache2
sudo systemctl disable apache2
```

### Configure MariaDB server

1. Start MariaDB:

```bash
sudo service mysql start
```

1. Configure MariaDB

```bash
mysql_secure_installation
```

### Configure PHP

1. Restart Apache

```bash
sudo service apache2 restart
```

1. Create an info.php file in your project folder with the following content:

```bash
<?phpphpinfo();
```

#### Configure phpMyAdmin

1. Install package

```bash
sudo apt-get install phpmyadmin
```

Select Apache, Yes to use dbconfig-common, enter MariaDB root password, choose password for phpMyAdmin itself

1. Enable necessary PHP extensions:

```bash
sudo phpenmod mcryptsudo phpenmod mbstring
```

1. Restart Apache

```bash
sudo service apache2 restart
```

#### Configure XDebug

1. Install package

```bash
sudo apt-get install php-xdebug
```

1. Turn XDebug on, open php.ini

```bash
sudo nano /etc/php/7.2/apache2/php.ini
```

1. Add the following lines:

```bash
[Xdebug]
zend_extension=xdebug.so
xdebug.remote_enable=1
xdebug.remote_host=localhost
xdebug.remote_port=9000
```

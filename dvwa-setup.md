# 📄 DVWA Setup Report (Terminal-Ready)

## 🖥️ Environment

- OS: Parrot OS (Debian-based Linux)
- Web Server: Apache2
- Database: MariaDB (MySQL compatible)
- Language: PHP
- Application: Damn Vulnerable Web Application (DVWA)

## 1️⃣ System Update & Preparation

```bash
sudo apt update && sudo apt upgrade -y
```

Install required packages:

```bash
sudo apt install -y apache2 mariadb-server php php-mysqli php-gd php-xml php-mbstring git
```

Start and enable services:

```bash
sudo systemctl start apache2
sudo systemctl enable apache2
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

Verify Apache is running:

```bash
systemctl status apache2
```

## 2️⃣ Secure MariaDB (Basic)

```bash
sudo mysql_secure_installation
```

Recommended choices:

- Set root password → Yes
- Remove anonymous users → Yes
- Disallow remote root login → Yes
- Remove test database → Yes
- Reload privilege tables → Yes

## 3️⃣ DVWA Download & Deployment

Move to web root:

```bash
cd /var/www/html
```

Clone DVWA repository:

```bash
sudo git clone https://github.com/digininja/DVWA.git
```

Rename directory (optional but clean):

```bash
sudo mv DVWA dvwa
```

Set ownership and permissions:

```bash
sudo chown -R www-data:www-data /var/www/html/dvwa
sudo chmod -R 755 /var/www/html/dvwa
```

## 4️⃣ Database Creation for DVWA

Login to MariaDB:

```bash
sudo mysql -u root -p
```

Create database and user:

```sql
CREATE DATABASE dvwa;
CREATE USER 'dvwauser'@'localhost' IDENTIFIED BY 'dvwapassword';
GRANT ALL PRIVILEGES ON dvwa.* TO 'dvwauser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

## 5️⃣ DVWA Configuration File

Navigate to config directory:

```bash
cd /var/www/html/dvwa/config
```

Copy default config file:

```bash
sudo cp config.inc.php.dist config.inc.php
```

Edit configuration:

```bash
sudo nano config.inc.php
```

Update database settings:

```php
$_DVWA[ 'db_server' ]   = 'localhost';
$_DVWA[ 'db_database' ] = 'dvwa';
$_DVWA[ 'db_user' ]     = 'dvwauser';
$_DVWA[ 'db_password' ] = 'dvwapassword';
```

Save and exit.

## 6️⃣ PHP Configuration Fixes

Edit PHP configuration:

```bash
sudo nano /etc/php/*/apache2/php.ini
```

Ensure the following values are set:

```ini
allow_url_fopen = On
allow_url_include = On
display_errors = On
```

Restart Apache:

```bash
sudo systemctl restart apache2
```

## 7️⃣ DVWA Initialization (Web)

Open browser:

```
http://localhost/dvwa/setup.php
```

Steps performed:

- Click Create / Reset Database
- Confirm database tables are created successfully

## 8️⃣ Verification Checks

Access DVWA login page:

```
http://localhost/dvwa
```

Default credentials:

- Username: admin
- Password: password

Post-login verification:

- PHP modules show green
- Database connection successful
- DVWA dashboard loads without errors

## ✅ Validation Commands

Check Apache logs:

```bash
sudo tail -f /var/log/apache2/access.log
```

Check Apache error logs:

```bash
sudo tail -f /var/log/apache2/error.log
```

Check MariaDB status:

```bash
systemctl status mariadb
```

## 📌 Result

DVWA was successfully:

- Installed
- Configured
- Connected to database
- Verified operational

The environment is now ready for controlled penetration testing labs.
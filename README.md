# lamp
Installation of LAMP and web application
[#!/bin/bash
if [ $(id -u) -ne 0 ];
then echo 'Please run with sudo or as root.'
exit 1
fi

# Install Apache, PHP, and PHP Modules
dnf -q install -y httpd php php-mysqlnd

# Start and enable the web server
systemctl start httpd
systemctl enable httpd

# Install MariaDB
dnf -q install -y mariadb-server

# Start and enable MariaDB
systemctl start mariadb
systemctl enable mariadb

# Create a wordpress database
mysqladmin create wordpress

# Create a user for the wordpress database
mysql -e "GRANT ALL on wordpress.* to wordpress@localhost identified by 'wordpress123';"
mysql -e "FLUSH PRIVILEGES;"

# Secure MariaDB
echo -e "\n\nrootpassword123\nrootpassword123\n\n\n\n\n" | mysql_secure_installation

# Download and extract WordPress
TMP_DIR=$(mktemp -d)
cd $TMP_DIR
curl -sOL https://wordpress.org/wordpress-5.5.1.tar.gz && tar zxf wordpress-5.5.1.tar.gz
mv wordpress/* /var/www/html

# Clean up cd /
/ rm -rf $TMP_DIR

# Install required dependencies
dnf -q install -y php-json
curl -sOL https://raw.github.com/wp-cli/builds/gh-pages/phar/wpcli.phar

# Move wp-cli.phar to /usr/local/bin and make it executable
mv wpcli.phar /usr/local/bin/wp
chmod 755 /usr/local/bin/wp


# Configure wordpress
cd /var/www/html
/usr/local/bin/wp core config --dbname=wordpress --dbuser=wordpress \ --
dbpass=wordpress123

# Install wordpress
/usr/local/bin/wp core install --url=http://10.23.45.60 \
--title="Blog" --admin_user="admin" --admin_password="admin" \
--admin_email="vagrant@localhost.localdomain"](https://us04web.zoom.us/j/74173536430?pwd=ZYeyGTbQaJ4LLW7wV116tR8GukmG8a.1)https://us04web.zoom.us/j/74173536430?pwd=ZYeyGTbQaJ4LLW7wV116tR8GukmG8a.1


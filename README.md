# Setting-Up-Virtual-Hosts

When using the Apache web server, you can use virtual hosts (similar to server blocks in Nginx) to encapsulate configuration details and host more than one domain from a single server. I will set up a domain called example.com, but you should replace this with your own domain name

**Create the directory for example**

> sudo mkdir /var/www/example

**Change/Assign ownership of the directory (example)**
> sudo chown -R $USER:$USER /var/www/example

The permissions of your web roots should be correct if you haven't modified your unmask value, but you can make sure by typing:
sudo chmod -R 755 /var/www/example

Make a new virtual host file at /etc/apache2/sites-available/example.conf

sudo nano /etc/apache2/sites-available/example.conf

Paste in the following configuration block, updated for our new directory and domain name:

<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName example
    ServerAlias example
    DocumentRoot /var/www/example
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

Save and close the file when you are finished.

Enable the file with a2ensite

sudo a2ensite example.conf

Restart Apache to implement your changes:

sudo systemctl restart apache2
# Triple Website Hosting
## This project sets up three websites on a single AWS instance using Apache HTTP server.

## *Prerequisites
An AWS instance with a public IP address

![image](https://github.com/user-attachments/assets/a5772bf8-acda-4c7e-a906-490930bdf50b)


A domain name (optional)

## Steps

### Step 1: Update the package list
```bash
sudo yum update -y
```
### Step 2: Install the HTTP server
```bash
sudo yum install httpd
```
### Step 3: Change to the Apache configuration directory
```bash
cd /etc/httpd/conf.d/
```
### Step 4: Configure virtual hosts

Create a virtualhosts.conf file with the following content:

```bash
sudo nano virtualhosts.conf
```
Add following content:

```bash
<VirtualHost *:80>
    ServerName web1.com
    ServerAlias www.web1.com
    DocumentRoot /var/www/web1
    <Directory /var/www/web1>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride None
        Require all granted
    </Directory>
</VirtualHost>

<VirtualHost *:80>
    ServerName web2.com
    ServerAlias www.web2.com
    DocumentRoot /var/www/web2
    <Directory /var/www/web2>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride None
        Require all granted
    </Directory>
</VirtualHost>

<VirtualHost *:80>
    ServerName web3.com
    ServerAlias www.web3.com
    DocumentRoot /var/www/web3
    <Directory /var/www/web3>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride None
        Require all granted
    </Directory>
</VirtualHost>
```

### Step 5: Create directories for each website

```bash
sudo mkdir -p /var/www/web1 /var/www/web2 /var/www/web3
```

### Step 6: Create an index.html file
```bash
sudo nano index.html
```

### Step 7: Copy the index.html file to each website directory
```bash
sudo cp -r ~/index.html /var/www/web1 && sudo cp -r ~/index.html /var/www/web2 && sudo cp -r ~/index.html /var/www/web3
```

### Step 8: Change ownership of the website directories
```bash
sudo chown -R apache:apache /var/www/web1 /var/www/web2 /var/www/web3
```
### Step 9: Restart the HTTP server
```bash
sudo service httpd restart
```
### Step 10: Configure DNS
Create three separate A records, one for each website, pointing to the instance's public IP address.

![image](https://github.com/user-attachments/assets/9b0b1439-7807-46ca-ac2a-2a006b62c154)


## That's it! 🎉 You now have three websites hosted on a single AWS instance.
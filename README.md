# Fdroid_server_deploy

### Resource
* Ubuntu v22.04 (2CPU, 40GB HDD, 8Gb RAM)

### Prepare VM
```Bash
sudo apt update
sudo apt upgrade
sudo apt install android-sdk-platform-tools
sudo apt-get install androguard
sudo apt-get install fdroidserver
```

### Install Nginx
```Bash
sudo apt-get install nginx
service nginx restart
```

### Nginx config site
```Bash
sudo mkdir -p /var/www/vedroidrepo.tech/html
sudo chown -R $USER:$USER /var/www/vedroidrepo.tech/html
sudo chmod -R 755 /var/www/vedroidrepo.tech
sudo mkdir /etc/nginx/sites-available/
sudo mkdir /etc/nginx/sites-enabled/
sudo nano /etc/nginx/sites-available/vedroidrepo.tech 
###
server {
        listen 80;

        root /var/www/vedroidrepo.tech/html/repo;
        index index.html;

        server_name vedroidrepo.tech www.vedroidrepo.tech;

        location / {
                try_files $uri $uri/ =404;
        }
}
###
sudo nano /etc/nginx/nginx.conf
# add to down

        ##
        # Virtual Host Configs
        ##

        include /etc/nginx/sites-enabled/*;
        include /etc/nginx/sites-enabled/*;
}

sudo ln -s /etc/nginx/sites-available/vedroidrepo.tech /etc/nginx/sites-enabled/
sudo nginx -s reload
```

### Initial fdroid repo
```Bash
cd /var/www/vedroidrepo.tech/html
export ANDROID_HOME=/usr/lib/android-sdk
fdroid init
sudo nano config.yml 
# Change url and name
repo_url: https://vedroidrepo.tech
repo_name: My First F-Droid Repo Demo
#
fdroid update
```

### Download apk
```Bash
cd /var/www/vedroidrepo.tech/html/repo
wget -q https://github.com/Darkempire78/OpenCalc/releases/download/v2.3.1/OpenCalc.v2.3.1.apk
wget -q https://f-droid.org/F-Droid.apk
fdroid update
```

### Check DNS
```
dig vedroidrepo.tech
```

### Certbot SSL
```Bash
sudo snap install --classic certbot
sudo certbot --version
sudo certbot --nginx --test-cert
# y
# n
sudo certbot --nginx
# 2 (Renew)
#Clear
sudo certbot renew --dry-run
```

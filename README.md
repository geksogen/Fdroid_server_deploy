# Fdroid_server_deploy

### Set k8s for Yandex Cloud use RKE

* Ubuntu v22.04 (2CPU, 40GB HDD, 8Gb RAM)
* fdroid v

### Prepare VM
```Bash
sudo apt update
#sudo apt upgrade
sudo apt install android-sdk-platform-tools
sudo apt-get install androguard
sudo apt-get install fdroidserver
```
#skip
### Install Nginx
```Bash
sudo apt-get install nginx
nano /etc/nginx/sites-available/default
```
### Config Nginx
```Bash
root /var/www/html/fdroid;

  location / {
  # включаем листинг директорий
  autoindex on;
  }
```
```Bash
service nginx restart
cd /var/www/html
rm -rf index.nginx-debian.html
```
#skip
### Initial repo fdroid
```Bash
export ANDROID_HOME=/usr/lib/android-sdk
#mkdir /var/www/html/fdroid
#sudo chown -R $USER /var/www/html/fdroid
cd /var/www/devopsbyexample.io/html/
rm -rf index.html
fdroid init
cd /repo
wget -q https://github.com/Darkempire78/OpenCalc/releases/download/v2.3.1/OpenCalc.v2.3.1.apk
cd ..
fdroid update -c
fdroid update
sudo nano config.yml
fdroid update
```

```Bash
repo_url = "http://<IP>/fdroid"
repo_url: https://localhost/fdroid/repo
repo_name: F-Droid Repo Demo

```

### download apk
```Bash
cd /repo

wget -q https://f-droid.org/F-Droid.apk
```

### Index and sign
```Bash
cd ../
fdroid update --create-metadata

```

### SSL Nginx
```Bash
sudo apt update
sudo mkdir -p /var/www/vedroidrepo.tech/html
sudo chown -R $USER:$USER /var/www/vedroidrepo.tech/html
sudo chmod -R 755 /var/www/vedroidrepo.tech
cd /var/www/devopsbyexample.io/html/ # wil be fdroid repo
nano index.html
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
# add to down }
include /etc/nginx/sites-enabled/*;
include /etc/nginx/sites-enabled/*;
sudo ln -s /etc/nginx/sites-available/vedroidrepo.tech /etc/nginx/sites-enabled/
sudo nginx -s reload
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

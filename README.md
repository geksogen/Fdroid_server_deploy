# Fdroid_server_deploy

### Set k8s for Yandex Cloud use RKE

* Ubuntu v22.04 (2CPU, 40GB HDD, 8Gb RAM)
* fdroid v

### Prepare VM
```Bash
sudo apt update
sudo apt upgrade
sudo apt install android-sdk-platform-tools
sudo apt-get install androguard
sudo apt-get install fdroidserver
```
### Установка Nginx
```Bash
sudo apt-get install nginx
nano /etc/nginx/sites-available/default
```
### Конфигурация Nginx
```Bash
root /var/www;

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

### Инициализация repo fdroid
```Bash
cd /var/www/html
fdroid init -v
```

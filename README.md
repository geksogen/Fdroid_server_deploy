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
nano /etc/nginx/sites-available/default
```
### Конфигурация Nginx
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

### Инициализация repo fdroid
```Bash
export ANDROID_HOME=/usr/lib/android-sdk
mkdir /var/www/html/fdroid
sudo chown -R $USER /var/www/html/fdroid
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

### Скачиваем apk в стор
```Bash
cd /repo

wget -q https://f-droid.org/F-Droid.apk
```

### Индексация и подпись apk
```Bash
cd ../
fdroid update --create-metadata

```

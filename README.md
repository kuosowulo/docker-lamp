# build LAMP by Docker Compose
用docker compose建置一個基本的LAMP環境。

一共啟動五個容器包含有:

- PHP:7.3
- Apache
- MySQL:8.0
- phpMyAdmin
- Redis

<br>
<br>

# Installation

1. clone 本專案到本地端
```
git clone https://github.com/kuosowulo/docker-lamp.git
```

<br>

2. 到專案資料夾內複製一個 .env
```
cd docker-lamp/
cp .env.example .env
```

<br>

3. 用 docker-compose 建立容器
```
docker-compose up -d
```

到此LAMP環境已經建置完成，可以透過 127.0.0.1 或是 http:localhost 訪問你的環境。


<br>
<br>

# PHP
已安裝套件:
- mysqli
- pdo_sqlite
- pdo_mysql
- mbstring
- zip
- intl
- mcrypt
- curl
- json
- iconv
- xml
- xmlrpc
- gd

<br>

若你想安裝更多套件可以到 ./bin/webserver/Dockerfile 新增任何你想要的套件，並且重啟 container 即可。
```
docker-compose build
```

<br>
<br>

# WebServer
Apache 的 port 被指定為 80，可以用 http://localhost:80/ 查看 phpinfo ，若是 80 port 被佔用或是想做更換可以到 .env 檔裡設定。

container 裡的 Apache 目錄 /var/www/html 與本地端的 /www 目錄綁定，若要更改路徑可至 .env 檔裡更改。

container 裡的 Apache目錄 /etc/apache2/sites-enabled 與本地端的 /config/vhosts/ 綁定，若要更改路徑可至 .env 檔裡更改。

若要遠端連線進 web server 則可以用 docker-compose exec。
```
docker compose exec webserver bash
```
<br>
<br>

# Database
這邊使用mysql8.0版本。

container 裡的 data 與本地端 ./data/mysql 綁定。

container 裡的 log 與本地端 ./logs/mysql 綁定。

MySQL 的 root 密碼及一組新增的 user 帳號在 .env 檔裡設定。

<br>
<br>

# phpmyadmin
phpmyadmin 預設 port 為 80，port 和相關帳號密碼可以至 .env 檔做更改。

url : http://localhost:8080/

預設 root 帳號: root

預設 root 密碼: password

<br>
<br>

# Redis
Redis 預設 port 為 6379，可以至 .env 檔做更改。

<br>
<br>

# Network
啟動一個名為 backend 的 bridge network 供本專案裡的容器使用。

<br>
<br>

# 注意事項
- 若需要別的版本的 php 和 mysql 可以到 ./bin/ 裡新增名稱為版本名的資料夾並且在裡面放置 dockerfile，之後只要修改 .env 檔裡的版本參數就可以執行。
- 本專案做為本地端快速建置開發環境使用，如果要用做對外的環境則需要注意安全性問題來修改各種細項。 例如:
  - php handler: mod_php=> php-fpm
  - mysql user 帳號及 IP 限制

<br>

聯絡信箱: kuosowulo@gmail.com

參考來源: https://github.com/sprintcube/docker-compose-lamp
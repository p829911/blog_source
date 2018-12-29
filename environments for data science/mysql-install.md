---
title: mysql install
date: 2018-12-06 21:52:38
tags:
- Ubuntu
- Mysql
categories:
- Mysql
---

### mysql install

```bash
sudo apt install -y mysql-server
```

```bash
sudo mysql_secure_installaion
```

press y|Y for Yes, any other key for No: n

remove anonymous users? y

disallow root login remotely? n

remove test database and access to it? n

reload privilege tables now? y

success!



```bash
sudo mysql
```

#### passward 설정

```mysql
SELECT user,authentication_string,plugin,host FROM mysql.user;
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password
BY 'dss';
FLUSH PRIVILEGES;
```

#### root 사용자로 접속

```mysql
mysql -u root -p
# 패스워드 입력
```

#### 상태확인

bash 창에서

```bash
sudo systemctl status mysql
```

active 확인

#### 외부접속 설정

```bash
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
```

bind-address = 0.0.0.0으로 수정

외부접속이 허용되도록 mysql 설정

```bash
mysql -u root -p
```

```mysql
grant all privileges on *.* to 'root'@'%' identified by '<password>';
```

#### 포트 활성화

AWS서버에서 3306포트 활성화

재시작으로 설정 적용

```bash
sudo systemctl restart mysql.service
```

mysql에서 접속

#### import sql file

바로 데이터 베이스 넣기

```bash
mysql -u root -p world < world.sql
```

mysql shell에서 넣기

```mysql
create database world;
use world;
source world.sql;
show tables;
```



#### Mysql 삭제

```bash
sudo apt remove --purge mysql-server mysql-client
sudo rm -rf /etc/mysql/var/lib/mysql
sudo apt autoremove
sudo apt autoclean
sudo apt purge mysql*
```


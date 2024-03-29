
### DB 서버 설정

- DB 서버 설치 및 설정을 아래와 같이 진행한다.

#### Step 1 > 소스 다운로드

```console

   $ git clone https://github.com/kin3303/CloudbeesCDRO
   $ cd CloudbeesCDRO
   $ git checkout master
```


#### Step 2 > DB 설치

```console
   $ sudo su
   $ cd data/mysql
   $ chmod 777 install_mysql.sh
   $ ./install_mysql.sh
   ...
   2022-04-20T06:49:43.493666Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: 초기패스워드
   ...
```

#### Step 3 > DB 설정 (새로운 터미널 열어 설정)

```console
   > /usr/local/mysql/bin/mysql -uroot -p 
   Enter password: 초기패스워드
   > ALTER USER 'root'@'localhost' IDENTIFIED BY '[신규패스워드]';
   > CREATE USER 'ecuser'@'%' IDENTIFIED BY '[신규패스워드]';
   > CREATE DATABASE IF NOT EXISTS ecdb;
   > CREATE DATABASE IF NOT EXISTS ecdb_upgrade;
   > GRANT ALL PRIVILEGES ON ecdb.* TO 'ecuser'@'%';
   > GRANT ALL PRIVILEGES ON ecdb_upgrade.* TO 'ecuser'@'%';
   > FLUSH PRIVILEGES;
   > exit;
```

#### Step 4 > 서비스 실행 등록 확인

```console
   $ reboot
   $ systemctl status mysqld
   $ /usr/local/mysql/bin/mysql -uroot -p
```

#### Step 5 > DB 백업 (필요시 사용)

- mysqlbkup.cnf 의 password='password!@#' 구문을 실제 password 로 변경 후 시도한다.

```console
   $ sudo su
   $ cd data/mysql
   $ chmod 777 bkup_mysql.sh
   $ ./bkup_mysql.sh
```


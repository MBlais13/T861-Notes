
## Basic Docker
Exec into 
```bash
docker exec -it mariadbprime mariadb -u root -p
```

`/etc/mysql/mariadb.conf.d/50-server.cnf`

```sql
docker inspect mariadbprime | grep IPAddress

docker exec -it mariadbslave mariadb -u root -p

SHOW SLAVE STATUS\G;

SELECT user, host FROM mysql.user;



STOP SLAVE;
CHANGE MASTER TO
  MASTER_HOST='172.17.0.8',
  MASTER_USER='replica',
  MASTER_PASSWORD='Welcome2020',
  MASTER_LOG_FILE='mysql-bin.000001',
  MASTER_LOG_POS=2297;
START SLAVE;


```




```sql
CREATE DATABASE lab4;

USE lab4;

CREATE TABLE students (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(20), email VARCHAR(50));

INSERT INTO students (name,email) VALUES ("Max","max@email.com"),("John","john@email.com");

CREATE USER 'webprocessor'@'%' IDENTIFIED BY 'Welcome2020';

GRANT ALL PRIVILEGES ON lab4.* TO 'webprocessor'@'%';
```


```sql
CREATE TABLE demons (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(20), uid VARCHAR(32));

INSERT INTO demons (name,uid) VALUES ("sirmax","d9a09ab1-5eb1"),("sirjohn","9a0fe9c4-15f3");

```

```sql

CREATE TABLE minions (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(20), color VARCHAR(50));

INSERT INTO minions (name,color) VALUES ("minion1","yellow"),("minion2","yellowbrown");

```


`mariadb-dump -u root -p"Welcome2020" --all-databases 172.17.0.10 > AllDB.sql`
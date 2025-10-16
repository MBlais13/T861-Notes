
```table-of-contents
title: **Table Of Contents:**
style: nestedList
minLevel: 0
maxLevel: 3
includeLinks: true
hideWhenEmpty: false
debugInConsole: false
```

---

# Install and Basic Config
```bash
sudo apt install mariadb-client mariadb-server
sudo mysql_secure_installation # interactive install
sudo systemctl enable mariadb
sudo systemctl start mariadb
```
Connect locally or remotely:
```bash
mariadb -u root -p
mariadb -u bob -p"drowssap" --host=php.scweb.ca --port=3306
```
> Note: `-p` must be directly before the password (no space).

---

# Database Management
## Create / Select / Drop
```sql
CREATE DATABASE mit550;

SHOW DATABASES;
USE mit550;

DROP DATABASE mit550;
```

## Export / Import
```bash
mariadb-dump -u root -p"pass" --all-databases > alldb.sql
mariadb -u root -p"pass" < alldb.sql
```

---

# User Management
## Creating Users
```sql
CREATE USER 'student'@'localhost' IDENTIFIED BY 'password';
CREATE USER 'student'@'%' IDENTIFIED BY 'password';  /* Allow from any host */
CREATE USER 'student'@'%.scweb.ca' IDENTIFIED BY 'password';  /* Allow all from scweb.ca */
CREATE USER 'student'@'192.168.%.%' IDENTIFIED BY 'password'; /* Allow any 192.168 subnet */
```

## Viewing Users
```sql
SELECT user,host,password FROM mysql.user;
```

## Privileges
```sql
GRANT ALL PRIVILEGES ON mit550.* TO 'student'@'%';   /* full access */
GRANT SELECT ON exampledb.* TO 'student'@'localhost'; /* read-only */
FLUSH PRIVILEGES;
```

## Show and Revoke Privileges
```sql
SHOW GRANTS FOR 'student'@'localhost';
REVOKE ALL ON exampledb.* FROM 'student'@'localhost';
REVOKE SELECT ON proddb.* FROM 'student'@'localhost';
```

---

# Table Management
## Creating and Dropping Tables
```sql
CREATE TABLE employee (
  id INT NOT NULL AUTO_INCREMENT,
  firstname VARCHAR(20),
  lastname VARCHAR(20),
  department VARCHAR(20),
  PRIMARY KEY (id)
);

DROP TABLE employee;
```

## Insert / Update / Delete Records
```sql
INSERT INTO employee VALUES (DEFAULT, "Franco", "Iacobacci", "Networking");

UPDATE employee SET department="IT" WHERE id=1; /* without WHERE it will update all records */
UPDATE employee SET department="IT" WHERE lastname="Smith"; /* updates every record with lastname 'Smith' */

DELETE FROM employee WHERE id=1;
```

## Viewing Records
```sql
/* get the 'id' of the record you want to update/delete */
SELECT * FROM employee;
SELECT * FROM employee WHERE firstname='Bob';
SELECT * FROM employee ORDER BY id;
```

---

# Replication Setup
Replication allows changes on the **master** to be copied to the **replica**.
## Master Configuration
Edit `/etc/mysql/mariadb.conf.d/50-server.cnf`:
```ini
server-id = 1
log_bin   = /var/log/mysql/mysql-bin.log
```
In SQL (on master):
```sql
CREATE USER 'replica'@'%' IDENTIFIED BY 'reppassword';
GRANT REPLICATION SLAVE ON *.* TO 'replica'@'%';
FLUSH PRIVILEGES;
SHOW MASTER STATUS\G;
```
> Record the **Log File** and **Position** for the replica.

## Replica Configuration
Edit `/etc/mysql/mariadb.conf.d/50-server.cnf`:
```ini
server-id = 2
log_bin   = /var/log/mysql/mysql-bin.log
```
In SQL (on replica):
```sql
STOP SLAVE;
CHANGE MASTER TO
  MASTER_HOST='172.17.0.2',
  MASTER_USER='replica',
  MASTER_PASSWORD='reppassword',
  MASTER_LOG_FILE='mysql-bin.000001',
  MASTER_LOG_POS=1187;
START SLAVE;
SHOW SLAVE STATUS\G;
```

## Testing Replication
On master:
```sql
CREATE DATABASE lab4;
USE lab4;
CREATE TABLE students (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(20), email VARCHAR(30));
INSERT INTO students (name, email) VALUES ("Neo","neo@email.com"),("Ben","ben@email.com");
```
Verify on replica:
```sql
SHOW DATABASES;
SELECT * FROM lab4.students;
```

---

# Replication Role Swap
On the current master (to become replica):
```sql
STOP SLAVE;
CREATE USER 'swapreplica'@'%' IDENTIFIED BY 'swap123';
GRANT REPLICATION SLAVE ON *.* TO 'swapreplica'@'%';
SHOW MASTER STATUS\G;
```
On the current replica:
```sql
STOP SLAVE;
CHANGE MASTER TO
  MASTER_HOST='172.17.0.3',
  MASTER_USER='swapreplica',
  MASTER_PASSWORD='swap123',
  MASTER_LOG_FILE='mysql-bin.000002',
  MASTER_LOG_POS=500;
START SLAVE;
```

---

# Replication Troubleshooting
| Issue | Check | Fix |
|-------|--------|------|
| Slave not connecting | Master IP / port | Verify Docker bridge or container IP |
| Error in position | Wrong file or position | Re-run `CHANGE MASTER TO` with correct values |
| Slave stopped | `Slave_IO_Running: No` | Restart slave and verify credentials |
| Duplicate entries | Inserts on slave | Only write to master |
| No replication | User privileges | Ensure `REPLICATION SLAVE` granted |

---

# MariaDB in Docker
These commands mimic the same replication setup but using Docker containers.

## Create Containers
```bash
docker pull mariadb
docker create --name mariadb-prime --restart always -e MYSQL_ROOT_PASSWORD=password mariadb
docker create --name mariadb-slave --restart always -e MYSQL_ROOT_PASSWORD=password mariadb

docker start mariadb-prime
docker start mariadb-slave

docker inspect mariadb-prime | grep IPAddress
```

## Connect and Configure
Enter each container shell:
```bash
docker exec -it mariadb-prime mariadb -u root -p
docker exec -it mariadb-slave mariadb -u root -p
```
Run normal replication SQL commands as before.

## Example Table Data
```sql
CREATE DATABASE lab4;
USE lab4;
CREATE TABLE students (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(20), email VARCHAR(50));
INSERT INTO students (name,email) VALUES ("Max","max@email.com"),("John","john@email.com");

CREATE TABLE demons (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(20), uid VARCHAR(32));
INSERT INTO demons (name,uid) VALUES ("sirmax","d9a09ab1-5eb1"),("sirjohn","9a0fe9c4-15f3");

CREATE TABLE minions (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(20), color VARCHAR(50));
INSERT INTO minions (name,color) VALUES ("minion1","yellow"),("minion2","yellowbrown");
```

## Copy All Databases from Container
```bash
mariadb-dump -u root -p"Welcome2020" --all-databases 172.17.0.10 > AllDB.sql
```

---
# Other
## Resetting Root Password
1. Stop MariaDB:
```bash
sudo systemctl stop mariadb
```
2. Start with grant tables disabled:
```bash
sudo mysqld_safe --skip-grant-tables &
```
3. Log in and reset:
```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'newpassword';
FLUSH PRIVILEGES;
```
4. Restart service:
```bash
sudo systemctl restart mariadb
```

## Common Exam Tasks
Quick reference of common operations you might need during the test.

| Task                    | Command                                                                                                       |
| ----------------------- | ------------------------------------------------------------------------------------------------------------- |
| **Create user**         | `CREATE USER 'user1'@'%' IDENTIFIED BY 'pass';`                                                               |
| **Grant privileges**    | `GRANT ALL PRIVILEGES ON db1.* TO 'user1'@'%'; FLUSH PRIVILEGES;`                                             |
| **Show grants**         | `SHOW GRANTS FOR 'user1'@'%';`                                                                                |
| **Dump all DBs**        | `mariadb-dump -u root -p"pass" --all-databases > alldb.sql`                                                   |
| **Restore DB**          | `mariadb -u root -p"pass" < alldb.sql`                                                                        |
| **Set up replication**  | configure master/replica in `50-server.cnf`, then use `CHANGE MASTER TO ...`                                  |
| **Check replication**   | `SHOW MASTER STATUS\G` and `SHOW SLAVE STATUS\G`                                                              |
| **Reset root password** | stop service → `mysqld_safe --skip-grant-tables &` → `ALTER USER 'root'@'localhost' IDENTIFIED BY 'newpass';` |

## Quick Reference Paths
| File | Purpose |
|------|----------|
| `/etc/mysql/mariadb.conf.d/50-server.cnf` | main server config |
| `/var/lib/mysql/` | database storage |
| `/var/log/mysql/mysql-bin.log` | replication binary log |
| `/etc/mysql/my.cnf` | general settings include file |
| `/root/.my.cnf` | optional user defaults |




## Installing and config
```sql
apt install mariadb-client, mariadb-server
```

```sql
mysql_secure_installation
```

```sql
mysql -u bob -p"drowssap"
```
`-p` then your password cannot have a space between

```sql
mysql -u bob -p"drowssap" --host=php.scweb.ca --port=3306
```

## Creating Users
```sql
CREATE USER 'student'@localhost IDENTIFIED BY 'password';
--
/* Allow users from any host */
CREATE USER 'student'@'%' IDENTIFIED BY 'password';

/* Allow users from any host that ends with scweb.ca */
CREATE USER 'student'@'%.scweb.ca' IDENTIFIED BY 'password';

/* Allow users from any IP that starts with 192.168 */
CREATE USER 'student'@'192.168.%.%' IDENTIFIED BY 'password';
```

### View Users
```sql
SELECT user,host,password FROM mysql.user;
```

## Privileges
```sql
/* Grant all privileges to student for the database mit416 and its tables */
GRANT ALL PRIVILEGES ON mit416.* to student@localhost

/* Grant read privileges to student on exampledb */
GRANT SELECT ON exampledb.* to student@localhost
```

### View Privileges
```sql
SHOW GRANTS FOR fiacobacci@localhost
```

### Remove Privileges
Remove privileges `REVOKE`
```sql
REVOKE ALL ON exampledb.* FROM student@localhost;
REVOKE SELECT ON proddb.* FROM student@localhost;
```


## Tables
### Create Tables
```sql
CREATE TABLE employee(
id INT NOT NULL AUTO_INCREMENT,
firstname VARCHAR(20),
lastname VARCHAR(20),
department VARCHAR(20),
PRIMARY KEY (id)
);
```

### Remove Tables
```sql
DROP TABLE employee;
```

### Inserting/Updating/Deleting Records
You can create records using `INSERT INTO`
Modify them with `UPDATE`
Remove them with `DELETE FROM`
```sql
/* Create a record */
INSERT INTO employee VALUES (DEFAULT,"Franco", "Iacobacci", "Networking");

/* Modify the record */
UPDATE employee SET department="IT" WHERE id=1;

/* Delete the record */
DELETE FROM employee WHERE id=1;
```

### Viewing Records
To View data you can use `SELECT`
```sql
/* Select all records from employee */
SELECT * FROM employee

/* Select all records with the first name Bob */
SELECT * FROM employee WHERE firstname='Bob'

/* Select all records and order by the ID */
SELECT * FROM employee ORDER BY id
```


## Export database
```sql
mysqldump -u username -p"password" database_name > File.sql
```

## Resetting the root password
1. Stop the mysqld service
2. Run `mysqld_safe --skip-grant-tables &`
3. Login to mysql shell using `mysql`
4. Update forgotten password using (see code below)
5. Restart service

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'newpassword';
FLUSH PRIVILEGES;
```
https://mariadb.com/docs/server/ha-and-performance/standard-replication/setting-up-replication

## Installing and config
First we have to add a server ID, and setup a log file and duration we keep the log, the ID must be unique
- From the log we can replicate changes that occurred while logging, however changes from before the log availability must be imported from a backup of the master database
- `SHOW MASTER STATUS\G`: allows you to view the status of the master server
- This command tells you crucial information about the replication process including the position and the file.
- `SHOW SLAVE STATUS\G`: gives us critical information about the slave server and any error messages that occur when attempting to replicate

- In order to setup a master you must use the following command
```sql
CHANGE MASTER TO
MASTER_HOST='172.17.0.2',
MASTER_USER='replica',
MASTER_PASSWORD='reppassword',
MASTER_LOG_FILE='mysql-bin.000001',
MASTER_LOG_POS=1187;
```

- The `CHANGE MASTER` command is used on the would be replica
- This identifies the host, user and password of the master database
- The command also identifies the log file on the `MASTER` server as well as the position in the log to start processing
- `START SLAVE` and `STOP SLAVE` are used to start the replication process
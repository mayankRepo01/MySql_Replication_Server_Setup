#### Master server configuration placed into “master/conf/mysql.conf.cnf”.
Here is some explaining. First 2 options are used to increase server performance and not related to the replication settings itself.
skip-host-cache
Disable use of the internal host cache for faster name-to-IP resolution.
skip-name-resolve
Disable DNS host name lookups
server-id = 1
For servers that are used in a replication, you must specify a unique server ID. It must be different from every other ID in use by any other source or replica.
log_bin = /var/log/mysql/mysql-bin.log
Enables bin log and sets the base name and path for the binary log files (like log_bin_basename).
binlog_format = ROW
Possible values are ROW (replica replay only actual changes on the row), STATEMENT (replica replay all the queries that changes the data), MIXED (statement-based replication is used unless server decides only row-based replication can give proper result, like replicating result of GUUID() ).
binlog_do_db = mydb
Specify a database, which statements will be written to binary log file.
Environment parameters related to launch MySQL in a docker container are placed into “master/mysql_master.env” file


#### Replica configuration.
Some of the configuration parameters repeat the Master database.
relay-log = /var/log/mysql/mysql-relay-bin.log
Contains database events, read from the source binary log.



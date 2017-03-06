# nagios-check_mysql_connections
Check the number of stablished connections to a MySQL database

Check MySQL Connections usage: 
```
./check_mysql_connections -w 15 -c 20 -u root -p 1234 -h database_host
```
Output: 
```
OK - 35 Database Connections |Connections=35;;;;
```

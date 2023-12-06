Настройка MySQL с ODBC

Установка компонентов на сервер
```
yum install unixODBC mariadb-connector-odbc

```

Поиск расположения файлов конфигурации

```
odbcinst -j
```
```
nano /etc/odbcinst.ini
```
```
[mysql]
Description = ODBC for MySQL
Driver      = /usr/lib/libmyodbc5.so
```
```
nano /etc/odbc.ini 
```
```
[test]
Description = MySQL test database
Driver      = mysql
Server      = 127.0.0.1
User        = root
Password    =
Port        = 3306
Database    = zabbix

```

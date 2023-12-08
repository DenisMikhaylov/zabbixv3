Устанавливаем zabbix server на второй сервер

```
apt install zabbix-server-mysql zabbix-agent
```

настраиваем базу данных mysql 

```
nano /etc/mysql/mariadb.conf.d/50-server.cnf
```
```
bind-address = 0.0.0.0
```
```
systemctl restart mariadb
```

Создаем подключение

```
mysql -uroot -p
create user zabbix@<ip address второго сервера> identified by 'password';
grant all privileges on zabbix.* to zabbix@<ip address второго сервера>;
```


Настраиваеам первый сервер

```
nano /etc/zabbix/zabbix_server.conf
```
```
HANodeName=zabbix-node1
NodeAddress=<ip address>:<port>
```
Перезапускаем сервер

```
systemctl restart zabbix-server
```

Проверяем работу

```
zabbix_server -R ha_status
```
или

На web report-sistem information

На втором сервере

```
nano /etc/zabbix/zabbix_server.conf
```
```
HANodeName=zabbix-node1
NodeAddress=<ip address>:<port>
DBHost=<ipaddress DB>
DPPassword=password
```

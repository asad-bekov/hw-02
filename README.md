# Установка Zabbix Server и Zabbix Agent
*Асадбеков Асадбек*

## Задание 1: 

Установка Zabbix Server 

## Процесс выполнения

1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
3. Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
4. Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.

### Команды:
```bash
sudo apt update
sudo apt install postgresql -y
sudo -u postgres psql
CREATE USER zabbix WITH PASSWORD '12345';
CREATE DATABASE zabbix OWNER zabbix;
\q
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_latest+debian11_all.deb
sudo dpkg -i zabbix-release_latest+debian11_all.deb
sudo apt update
sudo apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent -y
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
sudo sed -i 's/# DBPassword=/DBPassword=12345/g' /etc/zabbix/zabbix_server.conf
sudo systemctl restart zabbix-server zabbix-agent apache2
sudo systemctl enable zabbix-server zabbix-agent apache2
```

## Задание 2

Установите Zabbix Agent на два хоста.

## Процесс выполнения

1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
5. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

![alt text](https://github.com/asad-bekov/hw-02/blob/main/img/img1.png)
![alt text](https://github.com/asad-bekov/hw-02/blob/main/img/img2.png)
![alt text](https://github.com/asad-bekov/hw-02/blob/main/img/img3.png)
![alt text](https://github.com/asad-bekov/hw-02/blob/main/img/img4.png)
![alt text](https://github.com/asad-bekov/hw-02/blob/main/img/img5.png)



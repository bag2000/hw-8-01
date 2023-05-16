## Система мониторинга Zabbix - FOPS-10 - Поляков Роман
## Задание 1
### Cкриншот авторизации в админке
![Ссылка 1](https://github.com/bag2000/hw-8-01/blob/main/zab-ag-01.png)
  
### Текст использованных команд
sudo apt install postgresql  
  
wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_6.4-1+debian11_all.deb  
sudo dpkg -i zabbix-release_6.4-1+debian11_all.deb  
sudo apt update  
  
sudo apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts  
  
sudo -u postgres createuser --pwprompt zabbix  
sudo -u postgres createdb -O zabbix zabbix  
  
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix  
  
sudo nano /etc/zabbix/zabbix_server.con  
DBPassword=1234567890  
  
sudo systemctl restart zabbix-server apache2  
sudo systemctl enable zabbix-server apache2  
  
## Задание 2
### Скриншот раздела Сбор данных > Узлы сети
![Ссылка 2](https://github.com/bag2000/hw-8-01/blob/main/zab-ag-01.png)
  
### Скриншот лога zabbix agent
![Ссылка 3](https://github.com/bag2000/hw-8-01/blob/main/zab-ag-02.png)
  
### Скриншот раздела Мониторинг > Последние данные
![Ссылка 4](https://github.com/bag2000/hw-8-01/blob/main/zab-ag-03.png)
  
![Ссылка 5](https://github.com/bag2000/hw-8-01/blob/main/zab-ag-04.png)
  
### Текст использованных команд
wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_6.4-1+debian11_all.deb  
sudo dpkg -i zabbix-release_6.4-1+debian11_all.deb  
sudo apt update  
  
apt install zabbix-agent  
  
sed -i '/^Server=/d' /etc/zabbix/zabbix_agentd.conf  
sed -i '/^ServerActive=/d' /etc/zabbix/zabbix_agentd.conf  
sed -i '/^Hostname=/d' /etc/zabbix/zabbix_agentd.conf  
  
sed -i '1i Server=192.168.12.21' /etc/zabbix/zabbix_agentd.conf  
sed -i '2i Hostname=Agent1' /etc/zabbix/zabbix_agentd.conf  
  
systemctl restart zabbix-agent  
systemctl enable zabbix-agent  

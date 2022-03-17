# Setup MySQL database
- Install MySQL server
- Enable MySQL server to start with system
- Allow MySQL communiction on firewalld
```console
yum -y install mysql-server
systemctl enable --now mysqld
firewall-cmd --permanent --add-service mysql && firewall-cmd --reload
```
- Download sample world database
```console
curl -L -o world-db.tar.gz https://downloads.mysql.com/docs/world-db.tar.gz
tar xvf world-db.tar.gz
```
- Load sample world database
- Create MySQL account to be used for the sample application
```console
mysql -u root
CREATE USER 'cityapp'@'%' IDENTIFIED BY 'Cyberark1';
GRANT ALL PRIVILEGES ON *.* TO 'cityapp'@'%';
SOURCE /root/world-db/world.sql
SHOW DATABASES;
SELECT user,host FROM mysql.user;
QUIT;
```
- Verify
```console
ls -l /var/lib/mysql/world
```
- Clean-up
```console
rm -rf world-db.tar.gz world-db .mysql_history
```

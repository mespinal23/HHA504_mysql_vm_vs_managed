Ordered steps you executed, with command snippets
# Steps
## 1. OS Update 
a. **SSH into your VM** (terminal).  
b. **Update OS and Install MySQL**: To update, type in the following in your terminal:
   ```bash
   sudo apt-get update
   ```
 ```bash
 sudo apt install mysql-server mysql-client nano -y
   ```
 ```bash
 sudo mysql
   ```  
c. **In MySQL: Create User and Grant Privileges**:  
   ```bash
create user 'melojelo'@'%' identified by 'melojelo2025';
   ```
 ```bash
select * from  mysql.user;
   ```  
 ```bash
select * from  mysql.user \G
   ```  
 ```bash
grant all privileges on *.* to 'melojelo'@'%' with grant option;
   ```
 ```bash
select * from  mysql.user where user like 'melojelo' \G
   ```
```bash
show databases;
   ```
```bash
create database melojelo;
   ```
```bash
use melojelo;
   ```
```bash
show databases;
```
d. **Binding IP Address : Configuration**
```bash
sudo apt install nano
```
```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```
* Troubles you hit and how you solved them


* Start-to-finish elapsed time (minutes) measured by you


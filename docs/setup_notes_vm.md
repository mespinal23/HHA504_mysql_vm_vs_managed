Ordered steps you executed, with command snippets
# Steps
## OS Update 
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
> [!TIP]
> **When starting the binding IP section, close the terminal and reopen. You will run into errors if you miss this step.**

d. **Binding IP Address : Configuration**

```bash
sudo apt install nano
```
```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```
* change **bind address** to **0.0.0.0**
* change **mysqlx-bind-address** to **0.0.0.0**
     * **^O** (control O) to save
     * Click **Enter** to make sure it saves
     * **^X** (Control X) to exit

> [!NOTE]
> **In order for the change to occur you need to do a restart. Close the terminal and reopen before doing this step.**

e. **Restart**
```bash
sudo systemctl restart mysql
```
```bash
mysql -u melojelo -h External IP Address -p
```
   * **Enter password**
```bash
show databases;
```
## Troubles Encountered 
After completing some steps, I had to close and reopen the SSH terminal to make sure everything was installed and working properly.

## Start-To Finish Time
Total Time: 


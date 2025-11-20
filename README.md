# HHA504_mysql_vm_vs_managed
## MySQL on VM vs Managed Service

## **VM Service Cloud**

 * **GCP:** Compute Engine

   * **Region:** us-central1 (Iowa)
   * **Machine Type:** E2 (e2-small)
   * **OS:** Ubuntu (10GB is enough for SQL to run smoothly)

* **Firewall Rule:**
   * **Name:** mysql-connection- allow
   * **Description:** allows mysql port
   * **Targets:** All instances in the network
   * **IPv4 ranges:** 0.0.0.0/0

> [!NOTE]
> **0.0.0.0/0 is a wild card. It allows all ingress.**

## **Managed Service Cloud**

* **Azure:** Azure Database for MySQL – Flexible Server
   * **Server name:** mysqlassignment
   * **Region:** (US) West US 3
   * **Administrator log in:** dba
   * **Password:**
   * **Workload details:** Dev/Test
   * **Click on Add firewall rule for IP address**

## High-level steps to reproduce
- Create a small VM in GCP (Ubuntu), install MySQL, create user & DB, open port 3306 and use SSH tunnel.
- Create managed MySQL instance in Azure cloud, create admin user & DB
- Add your credentials in a local `.env` (use `.env.example`).
- Run
 ```bash
   python -m venv venv
   ```
```bash
   source venv/bin/activate
```
   
I did not run `python scripts/vm_demo.py` and `python scripts/managed_demo.py, I felt stuck at this point in the assignment and did not complete.

## Connection string patterns (no secrets)
- PyMySQL: `mysql+pymysql://USER:PASS@HOST:PORT/DBNAME`
    - This section gave an error and said no such file or directory

## How secrets stored locally
- Store real credentials in `.env` (ignored by .gitignore) 

## Screenshots
- `screenshots/vm/` — VM console, firewall, `systemctl status mysql`, mysql prompt
- `screenshots/managed/` — managed instance creation, connection info, authorized networks
- `screenshots/run/` — output of `vm_demo.py` and `managed_demo.py`

## Demo video
- [Loom/Zoom link here] (2–4 minute recording showing repo + running both scripts)


### 10) Safety & Clean-up
* Stop or delete the VM and managed instance after you finish to avoid costs.

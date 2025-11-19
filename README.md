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
     



> [!NOTE]
> **You must use a public IP (for demo): remember to delete resources after submission. They are expensive.**
* 
* `README.md` with:

  * Cloud chosen and region
  * Public high-level steps to reproduce (bullets)
  * Connection string patterns (no secrets), and how you stored secrets locally
  * Screenshots summary and links

* `scripts/vm_demo.py` and `scripts/managed_demo.py` that (you can just copy and paste the provided files, and or modify them as you like):

  1. Read credentials from environment (`.env`)
  2. Connect to MySQL via SQLAlchemy
  3. Create a new database (e.g., `dummydb`) if not exists
  4. Create a table (e.g., `visits`) via pandas `to_sql`
  5. Insert 5–10 rows from a pandas DataFrame
  6. Read back with `pd.read_sql` and print row count

* `docs/setup_notes_vm.md` and `docs/setup_notes_managed.md`:
  * Ordered steps you executed, with command snippets
  * Any config files you edited (e.g., `mysqld.cnf`), with the exact lines
  * Troubles you hit and how you solved them
  * **Start-to-finish elapsed time** (minutes) measured by you
* `docs/comparison.md`:
  * A short paragraph on which you would choose in production and why
* `screenshots/` evidence:

  * VM: portal/console creation page, package install, service status, firewall rules/security group, MySQL prompt proving DB/table exist, and a local or bastion test
  * Managed: creation wizard summary, connection info, authorized networks/VPC, connectivity test, metrics/overview page
* 2–4 minute **recording** (Zoom/Loom link in README) showing:

  * Your repo
  * Running each script end-to-end (VM then Managed) and printed results

---

### 5) Task A — MySQL on a VM (Self-managed)

1. **Provision VM**

   * OS: Ubuntu LTS or Oracle Linux
   * Instance type: small (e.g., 1–2 vCPU, 2–4 GB RAM)
   * Open **TCP ports 22 and 3306** 
2. **Install & Configure MySQL**

   * Install server packages; enable and start service.
   * Set strong root password (or auth plugin).
   * Edit `mysqld.cnf` (bind-address), restart service.
   * Configure firewall/security group rules minimally; note your choices in `setup_notes_vm.md`.

3. **Test Locally or Inside of Cloud Console (VS Code in GCP) environment **

   * `mysql -u <user> -p -h 127.0.0.1 -P 3306` from VM
   * Optional: set up an SSH tunnel from your dev machine instead of opening 3306 publicly.

---

### 6) Task B — Managed MySQL

Create the provider’s managed MySQL with a small tier. Capture:

* Engine version, vCPU/RAM tier
* Network model (public IP allowlist)
* Initial admin user, DB name
* Any automatic backups/HA configuration chosen

---

### 7) Python: SQLAlchemy + pandas Template

Create a `.env` (do **not** commit) from `.env.example`:

```
# VM
VM_DB_HOST=10.0.1.10        # or 127.0.0.1 via SSH tunnel
VM_DB_PORT=3306
VM_DB_USER=class_user
VM_DB_PASS=change_me
VM_DB_NAME=class_db_netid

# Managed
MAN_DB_HOST=...
MAN_DB_PORT=3306
MAN_DB_USER=class_user
MAN_DB_PASS=change_me
MAN_DB_NAME=class_db_netid
```

**Connection URL patterns** (choose *one* driver and be consistent):

* PyMySQL: `mysql+pymysql://USER:PASS@HOST:PORT/DBNAME`
* mysqlclient: `mysql+mysqldb://USER:PASS@HOST:PORT/DBNAME`

**Snippet (adapt for vm vs managed):**

```python
# scripts/vm_demo.py (similar for managed_demo.py)
```

### 10) Safety & Clean-up

* Delete public ingress rules you created.
* Stop or delete the VM and managed instance after you finish to avoid costs.

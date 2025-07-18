 ✅ SOP: Setup a Virtual Linux Server for Web Application Testing
🔖 Document Version & Approval

| Version | Date       | Name           | Role       |
|---------|------------|----------------|------------|
| 1.0     | 2025-07-18 | AI Assistant   | Author     |
| 1.1     | TBD        | Reviewer Name  | Reviewer   |
| 1.1     | TBD        | Approver Name  | Approver   |

---
 📌 Purpose

This Standard Operating Procedure (SOP) outlines the standardized process for provisioning and configuring a virtual Linux server used for functional web application testing. The procedure ensures consistent setup, security compliance, and support for automated test environments.

---

 🔍 Scope

This SOP applies to IT administrators, DevOps engineers, QA testers, and system integrators who are responsible for setting up and managing virtual environments for testing web applications prior to production deployment.

---

🎯 Objectives

- Provision a virtual server on VirtualBox or VMware.
- Install Ubuntu Server 22.04 LTS as the base OS.
- Configure basic network, hostname, SSH, and firewall.
- Install a LAMP/LEMP stack to host test applications.
- Enable a secure, testable environment for web app QA.

---
🧾 Accountability Matrix

| Task | Responsible Party | Notes |
|------|-------------------|-------|
| VM Setup & OS Install | System Administrator | Initial provisioning |
| Network & Security | DevOps Team | SSH, UFW, Firewall |
| Stack Installation | QA / Dev Team | LAMP/LEMP |
| Testing Deployment | QA Team | Automation & app deployment |
| Documentation | Technical Writer | Update SOP repo |

---
📘 Definitions

| Term | Definition |
|------|------------|
| VM | Virtual Machine |
| SSH | Secure Shell |
| LAMP | Linux, Apache, MySQL, PHP |
| UFW | Uncomplicated Firewall |
| WebApp | Web Application |

 🛠️ Procedure Steps

Step 1: Pre-setup Planning

- **Select Hypervisor**: Use VirtualBox (open-source) or VMware Workstation.
- **Resource Allocation**:
  - CPU: 2 cores minimum
  - RAM: 2 GB (4 GB recommended)
  - Disk: 20 GB dynamically allocated
- **OS Image**: Download latest Ubuntu Server 22.04 LTS ISO.
- **Hostname**: `webapptest.local`
- **Network Mode**: Use *Bridged Adapter* or *NAT with Port Forwarding*.

---
Step 2: Create & Configure Virtual Machine

- Launch VirtualBox or VMware.
- Create a new VM:
  - Name: `webapp-test`
  - Type: Linux (Ubuntu 64-bit)
  - Attach ISO in optical drive.
- Start VM and proceed with OS installation:
  - Set static IP or DHCP.
  - Create a primary user (e.g., `tester`).
  - Enable OpenSSH Server when prompted.

---

 Step 3: Post-Installation Configuration

- SSH into the server:
  ```bash
  ssh tester@<ip-address>
  ```
- Update system:
  ```bash
  sudo apt update && sudo apt upgrade -y
  ```
- Configure hostname:
  ```bash
  sudo hostnamectl set-hostname webapptest.local
  ```

---

Step 4: Install Essential Web Stack

Choose one of the following based on your app:

Option A: LAMP Stack**
```bash
sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql -y
```

Option B: LEMP Stack**
```bash
sudo apt install nginx mysql-server php-fpm php-mysql -y
```

- Test the web server:
  ```bash
  curl http://localhost
  ```

---

- Configure UFW:
  ```bash
  sudo ufw allow OpenSSH
  sudo ufw allow 'Apache Full'  # Or 'Nginx Full'
  sudo ufw enable
  ```
- Enable fail2ban (optional):
  ```bash
  sudo apt install fail2ban
  sudo systemctl enable fail2ban
  ```

--- Step 6: Prepare for Testing

- Create `/var/www/html/testapp` or custom directory.
- Set permissions:
  ```bash
  sudo chown -R www-data:www-data /var/www/html/testapp
  ```
- Deploy test app (manually or CI/CD).

---

📎 Reference Documents

- [Ubuntu Server ISO](https://ubuntu.com/download/server)
- [Apache Documentation](https://httpd.apache.org/)
- [Nginx Guide](https://www.nginx.com/resources/wiki/start/)
- [MySQL Docs](https://dev.mysql.com/doc/)
- [PHP Manual](https://www.php.net/manual/en/)

---

 🗂️ Revision History

| Version | Date       | Changes Made By | Summary of Changes |
|---------|------------|------------------|---------------------|
| 1.0     | 2025-07-18 | AI Assistant     | Initial draft       |

---

 ✅ Notes

- You may optionally enable phpMyAdmin or install Node.js based on the test app framework.
- Always snapshot the VM after setup for backup.
- Clone this SOP into your GitHub markdown project and commit as `sop-webapp-linux-vm.md`.

# 🚀 DevOps Infrastructure Automation Project

## Terraform + Ansible + AWS EC2 + Nginx + Docker

---

# 📌 Project Overview

This project demonstrates an end-to-end DevOps workflow:

* Provision infrastructure using **Terraform**
* Configure server using **Ansible**
* Deploy application via **Git**
* Serve application using **Nginx**
* Install Docker for container readiness

This simulates a real-world Infrastructure → Configuration → Deployment pipeline.

---

# 🏗 Architecture

```
                ┌─────────────────────┐
                │   Developer (WSL)   │
                │ Terraform + Ansible │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │      AWS EC2        │
                │  Amazon Linux 2     │
                └──────────┬──────────┘
                           │
                ┌──────────┴──────────┐
                │   Ansible Config     │
                │ - Install Git        │
                │ - Install Docker     │
                │ - Install Nginx      │
                │ - Clone Git Repo     │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │   Nginx Web Server  │
                │  Static Web App     │
                └─────────────────────┘
```

---

# 🛠 Technologies Used

| Tool      | Purpose                  |
| --------- | ------------------------ |
| AWS EC2   | Compute Infrastructure   |
| Terraform | Infrastructure as Code   |
| Ansible   | Configuration Management |
| Nginx     | Web Server               |
| Docker    | Container Engine         |
| Git       | Version Control          |
| Linux     | Server Operating System  |

---

# ⚙️ Phase 1 – Infrastructure Provisioning (Terraform)

## 📁 Project Structure

```
aws-ec2-terraform/
│
├── provider.tf
├── variables.tf
├── main.tf
└── outputs.tf
```

## 🔹 What Terraform Created

* EC2 instance (t2.micro)
* Security Group (SSH + HTTP)
* Attached existing Key Pair
* Output public IP

## 🔹 Terraform Workflow

```bash
terraform init
terraform plan -var="key_name=Home-Key"
terraform apply -var="key_name=Home-Key"
```

## 🔹 Output

```
public_ip = 15.207.xx.xx
```

---

# ⚙️ Phase 2 – Configuration Management (Ansible)

## 📁 Project Structure

```
ansible-ec2-setup/
│
├── inventory.ini
└── playbook.yml
```

---

## 🔹 Inventory File

```ini
[web]
15.207.xx.xx ansible_user=ec2-user ansible_ssh_private_key_file=/home/aditya/.../Home-Key.pem
```

---

## 🔹 What Ansible Configured

* Updated packages
* Installed Git
* Installed Docker
* Started Docker service
* Installed Nginx
* Enabled Nginx via amazon-linux-extras
* Cloned Git repository
* Deployed static web application
* Fixed file permissions
* Restarted Nginx

---

## 🔹 Playbook Execution

```bash
ansible-playbook -i inventory.ini playbook.yml
```

---

# 🌐 Application Deployment

Git Repository:

```
https://github.com/ProgrammingProphet/devops-showcase-app.git
```

Deployment Flow:

```
Git Clone → /opt/devops-app
Copy → /usr/share/nginx/html
Set Permissions → nginx:nginx
Restart Nginx
```

Access via:

```
http://15.207.xx.xx
```

---

# 🐳 Docker Setup

Docker was installed and enabled:

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

Docker prepares the server for future containerized deployments.

---

# 🔍 Debugging & Troubleshooting (Key Learning)

During implementation, we solved:

### ✅ SSH Key Path Issue

* Absolute path required in Ansible inventory

### ✅ Case-Sensitive AWS Key Name

* `Home-Key` ≠ `Home-key`

### ✅ Nginx Package Not Found

* Required enabling via:

  ```
  amazon-linux-extras enable nginx1
  ```

### ✅ 403 Forbidden Error

* Caused by missing `index.html`
* Also handled file permission issues
* Verified via:

  ```
  sudo tail -n 20 /var/log/nginx/error.log
  ```

### ✅ Nested Git Directory Issue

* Corrected deployment path
* Ensured proper file copy structure

---

# 🔐 Security Considerations

* Used IAM user (not root account)
* Security group restricted to required ports
* Private key permission set to 400
* No credentials stored in code

---

# 📚 Key DevOps Concepts Demonstrated

✔ Infrastructure as Code
✔ Idempotent Configuration
✔ SSH Authentication
✔ Cloud Networking
✔ Linux Service Management
✔ Application Deployment Automation
✔ Error Log Analysis
✔ Nginx Debugging
✔ Git-based Deployment

---

# 🎯 What This Project Proves

This project demonstrates ability to:

* Provision cloud infrastructure programmatically
* Automate server configuration
* Deploy applications without manual intervention
* Debug Linux and web server issues
* Understand full DevOps lifecycle

---

# 🚀 Future Enhancements

* Add Terraform Remote Backend (S3 + DynamoDB)
* Convert Ansible playbook into Roles
* Containerize app with Docker
* Integrate Jenkins CI/CD pipeline
* Use Terraform modules
* Implement HTTPS via Let's Encrypt
* Add monitoring (CloudWatch)

---

# 🏆 Final Outcome

Fully automated:

```
Code → Infrastructure → Server Config → Application Deployment
```

Access the live application:

```
http://<EC2_PUBLIC_IP>
```

---

# 💡 Learning Reflection

Through this project, I learned:

* Real-world debugging techniques
* Importance of file permissions
* Cloud region and key pair sensitivity
* Difference between provisioning and configuration
* How DevOps tools integrate together

---


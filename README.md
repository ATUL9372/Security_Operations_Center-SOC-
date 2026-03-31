# 🚀 ELK Stack Deployment & Cleanup using Ansible

This project automates the **installation, configuration, and complete removal** of the ELK Stack (**Elasticsearch, Logstash, Kibana**) on an Ubuntu server using Ansible.

---

## 📌 Project Overview

This repository provides:

* ✅ Automated ELK Stack installation using `.deb` packages
* ✅ Basic configuration for HTTP (no SSL) setup
* ✅ Service management (start, enable)
* ✅ Full cleanup playbook (stop, disable, purge, delete data)
* ✅ Secure credential handling using Ansible Vault

---

## 🏗️ Architecture

```
Ansible Control Node
        |
        | SSH
        v
Target Ubuntu Server
   ├── Elasticsearch (9200)
   ├── Kibana (5601)
   └── Logstash (5044)
```

---

## 📂 Project Structure

```
.
├── inventory.ini
├── elk-install.yml
├── elk-cleanup.yml
├── secrets.yml   # Encrypted using Ansible Vault
└── README.md
```

---

## ⚙️ Prerequisites

* Ubuntu 22.04 / 24.04 server
* Ansible installed on control node
* SSH access to target machine
* Sudo privileges

---

## 🔐 Setup or Installations of Ansible

* [Ansible Installation Guide](https://docs.ansible.com/projects/ansible/latest/installation_guide/installation_distros.html)

``` bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible

```

## 🔐 Setup Secrets (Vault)

Set Default Editor = nano : [ Temporary ]

```bash
export EDITOR=nano
```

Set Default Editor = nano : [ Permanent ]

```bash
echo 'export EDITOR=nano' >> ~/.bashrc
source ~/.bashrc
```

Ansible Vault Help
```bash
ansible-vault --help
```

Create and encrypt secrets file:

```bash
ansible-vault create example.yml
```

Example content:

```yaml
ansible_user: <Target-Machine-Username>
ansible_password: <Target-Machine-Password>
ansible_become_password: <Target-Machine-Password>

kibana_user: "kibana" # kibana username
kibana_pass: "kibana" # kibana password

elastic_user: "elastic" # elasticsearch username
elastic_pass: "elastic" # elasticsearch password

```

Edit Existing Vault File

```bash
ansible-vault edit example.yml
```

Encrypt File (example.yml)

```bash
ansible-vault encrypt example.yml
```

Decrypt File

```bash
ansible-vault decrypt example.yml
```

View Without Decrypt

```bash
ansible-vault view example.yml
```

---

## 📦 ELK Installation

Run the playbook using J enter your ansible-valut password:

```bash
ansible-playbook -i inventory.ini elk-install.yml -J
```

Run the playbook using --ask-vault-pass
```bash
ansible-playbook -i inventory.ini elk-install.yml --ask-vault-pass
```
---

## 🌐 Access Services

* Elasticsearch → http://<server-ip>:9200
* Kibana → http://<server-ip>:5601

---

## 🧹 Cleanup / Uninstall ELK

This will:

* Stop services
* Disable services
* Remove packages
* Delete all configs, logs, and data

```bash
ansible-playbook -i inventory.ini elk-cleanup.yml -J
```

---

## ⚠️ Warning

> This cleanup playbook will permanently delete all Elasticsearch data.

Make sure to take a backup before running in production.

---

## 🛠️ Key Configurations

### Elasticsearch

* `network.host: 0.0.0.0`
* `http.port: 9200`
* Security disabled (for learning purpose)

### Kibana

* `server.port: 5601`
* `server.host: 0.0.0.0`
* `elasticsearch.hosts: ["http://localhost:9200"]`
* Connected to Elasticsearch via HTTP

### Logstash

* Beats input on port `5044`
* Output to Elasticsearch

---

## 🧪 Testing

Check connectivity:

```bash
ansible all -i inventory.ini -m ping
```

---

## 💡 Future Improvements

* 🔒 Enable HTTPS (TLS/SSL)
* 🔐 Enable X-Pack Security
* 📊 Integrate Filebeat / Metricbeat
* ☁️ Deploy on AWS EC2 with Terraform
* 📈 Add monitoring (Prometheus + Grafana)

---

## 👨‍💻 Author

**Atul Yadav**
DevOps Engineer | AWS | Ansible | Monitoring

---

## ⭐ Contribute

Feel free to fork this repo and improve it. Pull requests are welcome!

---

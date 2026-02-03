# MySQL to Amazon RDS Migration using EC2

**Author:** Om  
**Project Type:** AWS Cloud | Database Migration  
**Version:** 1.0  
**License:** MIT  

---

## 🌐 Project Overview
This project demonstrates how to migrate a **MySQL database from an EC2 instance to Amazon RDS (MySQL engine)**.  
It covers RDS setup, security configuration, export/import commands, and real-world best practices.

**🎯 Goal:** Secure and efficient MySQL migration to AWS RDS  
**🛠 Tools Used:** EC2, RDS, MySQL, AWS Console, AWS CLI  

---

## 🧩 Architecture
+--------------------+ +---------------------------+
| EC2 Instance | ----> | Amazon RDS (MySQL) |
| MySQL Installed | | Managed DB Service |
+--------------------+ +---------------------------+


---

## ⚙️ Tech Stack

| Component | Description |
|---------|-------------|
| ☁️ AWS EC2 | Compute instance hosting MySQL |
| 🗄️ AWS RDS | Managed MySQL database |
| 🐬 MySQL | Database engine |
| 🔐 Security Groups | Network access control |

---

## 🚀 Step-by-Step Setup

### 📌 Step 1 — Launch EC2 & Install MySQL
```bash
sudo apt update -y
sudo apt install mysql-server -y
sudo systemctl start mysql
sudo systemctl enable mysql
Create database and table:

CREATE DATABASE studentdb;
USE studentdb;

CREATE TABLE students (
  roll_no INT PRIMARY KEY,
  name VARCHAR(100),
  contact VARCHAR(15),
  address VARCHAR(255)
);
📌 Step 2 — Export MySQL Database
sudo mysqldump -u root -p studentdb > mydb.sql
📌 Step 3 — Create RDS MySQL Instance
Engine: MySQL

Instance: db.t3.micro

Public access: Yes (Demo)

Port: 3306

📌 Step 4 — Configure Security Group
Inbound Rule:

Type: MySQL/Aurora

Port: 3306

Source: EC2 Security Group

📌 Step 5 — Connect EC2 to RDS
sudo apt install mysql-client -y
mysql -h <rds-endpoint> -u admin -p
📌 Step 6 — Create Database in RDS
CREATE DATABASE studentdb;
📌 Step 7 — Import Database to RDS
mysql -h <rds-endpoint> -u admin -p studentdb < mydb.sql
📌 Step 8 — Verify Migration
USE studentdb;
SELECT * FROM students;
✅ Migration successful!

🧠 Common Issues & Fixes
Issue	Cause	Fix
Access denied	Wrong credentials	Use correct RDS username/password
Timeout	SG blocked	Allow port 3306
Import error	DB not created	Create DB before import
📁 Folder Structure
MYSQL-TO-RDS-MIGRATION-USING-EC2/
│
├── mydb.sql
├── README.md
├── LICENSE
└── Images/
🚀 Future Enhancements
Automate migration using AWS DMS

Enable Multi-AZ RDS

Add CloudWatch monitoring

Script-based automation

🧾 Key Learnings
AWS RDS connectivity

mysqldump-based migration

Secure EC2 ↔ RDS communication

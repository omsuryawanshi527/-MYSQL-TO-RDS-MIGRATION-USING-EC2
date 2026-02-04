# MySQL to Amazon RDS Migration using EC2

**Author:** Om  
**Project Type:** AWS Cloud | Database Migration   
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

🚀 Step-by-Step Implementation
📌 Step 1 — Launch EC2 & Install MySQL
sudo apt update -y
sudo apt install mysql-server -y
sudo systemctl start mysql
sudo systemctl enable mysql
Create sample DB:

CREATE DATABASE studentdb;
USE studentdb;

CREATE TABLE students (
  roll_no INT PRIMARY KEY,
  name VARCHAR(100),
  contact VARCHAR(15),
  address VARCHAR(255)
);

---


📌 Step 2 — Export EC2 MySQL Database
sudo mysqldump -u root -p studentdb > mydb.sql


➡️ Exports DB into mydb.sql.

---


📌 Step 3 — Create RDS MySQL Instance

Engine: MySQL

Template: Free Tier

Instance: db.t3.micro

Port: 3306

Public access: Yes (demo)

Wait until status becomes Available ✅

---


📌 Step 4 — Configure RDS Security Group (IMPORTANT)

Inbound rule:

Type	Port	Source
MySQL/Aurora	3306	EC2 Security Group

This allows only your EC2 to access RDS.

---


📌 Step 5 — Connect EC2 to RDS
sudo apt install mysql-client -y

mysql -h <rds-endpoint> -u admin -p


Example:

mysql -h myrdsdb.xxxxx.ap-south-1.rds.amazonaws.com -u admin -p

---

📌 Step 6 — Create Target DB on RDS
CREATE DATABASE studentdb;
EXIT;

📌 Step 7 — Import SQL File into RDS
mysql -h <rds-endpoint> -u admin -p studentdb < mydb.sql

---

📌 Step 8 — Verify Migration
USE studentdb;
SELECT * FROM students;

---

✅ Data successfully migrated.

🧠 Common Issues & Fixes
Issue	Cause	Fix
Connection hangs	Port 3306 blocked	Allow EC2 SG in RDS SG
Access denied	Wrong credentials	Use RDS admin user
Import fails	DB missing	Create DB before import

---

📊 Benefits

Secure EC2 → RDS migration

Reduced DB management overhead

Practical AWS networking experience

Real DevOps troubleshooting exposure

---

💡 Core Concepts Learned

EC2 hosted MySQL → RDS migration

mysqldump export/import

Security Group based connectivity

VPC level communication

AWS RDS administration
🚀 Future Enhancements

Automate migration using AWS Database Migration Service

Enable Multi-AZ for HA

Monitoring with Amazon CloudWatch

Scripted automation

# 💾 MYSQL-TO-RDS-MIGRATION-USING-EC2

**Author:** Avinash
**Project Type:** AWS Cloud | Database Migration  
**Version:** 1.1  
**License:** MIT  

---

## 🌐 Project Overview

This project demonstrates how to migrate a **MySQL database from an EC2 instance** to **Amazon RDS (MySQL engine)**.  
It covers **RDS setup, security configuration, export/import commands**, and best practices for real-world migrations.

**Goals:**  
- Move data securely and efficiently to AWS RDS  
- Understand EC2 ↔ RDS connectivity and security  

**Tools Used:** EC2, RDS, MySQL, AWS Console, CLI  

---

## 🧩 Architecture

+--------------------+ +---------------------------+
| EC2 Instance | --> | Amazon RDS (MySQL) |
| MySQL Installed | | Managed Database Service |
+--------------------+ +---------------------------+

yaml
Copy code

---

## ⚙️ Tech Stack

| Component | Description |
|-----------|-------------|
| ☁️ AWS EC2 | Compute instance hosting MySQL |
| 🗄️ AWS RDS | Managed MySQL database service |
| 🐬 MySQL | Database engine used for migration |
| 🔐 Security Groups | Network control for EC2 ↔ RDS access |

---

## 🚀 Step-by-Step Setup (Amazon Linux Version)

### Step 1 — Launch EC2 Instance

1. Launch **Amazon Linux 2** EC2 instance from AWS Console.
2. Connect via SSH:

```bash
ssh -i path/to/key.pem ec2-user@<EC2_PUBLIC_IP>

Update packages:
sudo yum update -y

Install MySQL server:
sudo yum install mysql-server -y

Start and enable MySQL service:
sudo systemctl start mysqld
sudo systemctl enable mysqld

Secure MySQL and create a sample database:
sudo mysql

CREATE DATABASE studentdb;
USE studentdb;

CREATE TABLE students (
  roll_no INT PRIMARY KEY,
  name VARCHAR(100),
  contact VARCHAR(15),
  address VARCHAR(255)
);

INSERT INTO students (roll_no, name, contact, address) 
EXIT;

Step 2 — Export the Local MySQL Database
sudo mysqldump -u root -p studentdb > mydb.sql

🧾 This creates a SQL dump file for migration.

Step 3 — Create an RDS MySQL Database
Go to AWS Console → RDS → Create Database
Choose Standard Create
Engine: MySQL
Template: Free Tier
DB Identifier: myrdsdb
Master username: admin
Master password: (create a secure password)
Instance class: db.t3.micro
Public access: ✅ Yes (for demo)
Port: 3306
Click Create Database and wait until status is Available ✅

Step 4 — Configure RDS Security Group
Go to EC2 → Security Groups
Find RDS security group
Edit Inbound Rules → Add Rule:
Type: MySQL/Auro
Port: 3306

Source: Your EC2’s security group (recommended)

Step 5 — Connect EC2 to RDS
Install MySQL client on EC2:
sudo yum install mysql -y

Test connection:
mysql -h <RDS_ENDPOINT> -u admin -p
Example:
mysql -h myrdsdb.cno4usiwkkw0.ap-south-1.rds.amazonaws.com -u admin -p

Step 6 — Create Target Database in RDS
CREATE DATABASE studentdb;
EXIT;

Step 7 — Import SQL File from EC2 to RDS
mysql -h <RDS_ENDPOINT> -u admin -p studentdb < mydb.sql

Step 8 — Verify Data Migration
mysql -h <RDS_ENDPOINT> -u admin -p
USE studentdb;
SELECT * FROM students;

✅ You should now see your table and data successfully migrated!

📁 Folder Structure

MYSQL-TO-RDS-MIGRATION-USING-EC2/
│
├── README.md        # Project documentation
└── Images/          # (Optional) Add setup screenshots

📸 Recommended Screenshots

RDS creation page
Security group inbound rules
EC2 MySQL connection success
SELECT * FROM students; output

🧾 Summary

✅ Created MySQL DB on EC2 (Amazon Linux)
✅ Exported database using mysqldump
✅ Created RDS MySQL instance
✅ Configured security for EC2 ↔ RDS communication
✅ Imported SQL file to RDS successfully

💡 Key Learning

Understanding AWS RDS connectivity
Using mysqldump for database migration
Setting up secure VPC communication between EC2 and RDS

⭐ Author
Avinash
```

[💼 LinkedIn]((https://www.linkedin.com/in/%F0%9D%99%B0%F0%9D%9A%9F%F0%9D%9A%92%F0%9D%9A%97%F0%9D%9A%8A%F0%9D%9A%9C%F0%9D%9A%91-%F0%9D%9A%89%F0%9D%9A%8A%F0%9D%9A%95%F0%9D%9A%94%F0%9D%9A%8E-1884b024a/)) 
• [✉️ Email](avinashzalake2@gmail.com) 
• [🐙 GitHub](https://github.com/avinashzalake2-cyber) 

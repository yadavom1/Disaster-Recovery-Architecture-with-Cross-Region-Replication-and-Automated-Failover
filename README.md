# Disaster-Recovery-Architecture-with-Cross-Region-Replication-and-Automated-Failover

This project demonstrates the implementation of a Disaster Recovery (DR) architecture using AWS services. It includes a primary region and a disaster recovery region with database replication, failover testing, and application connectivity using Node.js and MySQL.

---
# 🏗️ Architecture Overview

-Primary Region: EC2 instance + RDS MySQL database
-DR Region: RDS Read Replica (cross-region)
-Application: Node.js (Express)
-Database: MySQL (AWS RDS)
-Replication: Automated cross-region replication

# 🛠️ Technologies Used

-AWS EC2
-AWS RDS (MySQL)
-Node.js
-Express.js
-Git & GitHub
-MySQL Client / CLI

# 📁 Project Structure

project-folder/
│
├── app/
│   ├── app.js
│   ├── package.json
│
├── screenshots/
│   ├── replication-proof.png
│   ├── failover-test.png
│   ├── rds-endpoint.png
│
└── README.md

**📸ARCHITECTURE IMAGE**

![Image](https://github.com/user-attachments/assets/d92cb06b-b6f9-4993-8518-8f5cef8aa6d2)

# 🚀 Steps to Run the Project

1.Clone the repository
  git clone https://github.com/your-username/project-name.git

2.Navigate to project folder
  cd project-name

3.Install dependencies
  npm install

4.Run the application
  node app.js
  
5.Open in browser
  http://localhost:3000

# Replication Proof

- Created RDS database in primary region
- Created read replica in DR region
- Inserted data in primary DB
- Verified data automatically appeared in read replica

# Failover Testing

- Promoted read replica to standalone database
- Updated new database endpoint in application
- Application worked successfully with DR database

# RTO and RPO

RTO (Recovery Time Objective):
Time required to restore application after failure.

RPO (Recovery Point Objective):
Amount of data that can be lost during failure.

# Lessons Learned

- How to create RDS read replica
- How to test failover
- How to connect Node.js with RDS
- How to upload project to GitHub

# Step-by-Step Upload to GitHub

Step 1 – Open terminal inside project folder
         cd project-folder
         
Step 2 – Initialize Git
         git init
         
Step 3 – Add files
         git add .
         
Step 4 – Commit files
         git commit -m "Initial project upload"
         
Step 5 – Create repository on GitHub
         aws-disaster-recovery-project

Step 6 – Connect local project to GitHub 
         git remote add origin https://github.com/your-username/project-name.git

Step 7 – Upload project
         git branch -M main
         git push -u origin main

# Here are all commands + code (step-by-step) for your AWS Disaster Recovery Node.js + RDS project.

# 🚀 1. Create Node.js App

   Step 1 – Create project folder
            mkdir dr-project
            cd dr-project

   Step 2 – Initialize Node.js
           npm init -y

   Step 3 – Install dependencies
            npm install express mysql2

# 🧾 2. Create app.js

const express = require("express");
const mysql = require("mysql2");

const app = express();

// 🔹 Replace with your RDS endpoint
const db = mysql.createConnection({
  host: "your-rds-endpoint",
  user: "admin",
  password: "your-password",
  database: "testdb"
});

// Connect to DB
db.connect((err) => {
  if (err) {
    console.log("Database connection failed:", err);
  } else {
    console.log("Connected to RDS MySQL");
  }
});

// API route
app.get("/", (req, res) => {
  db.query("SELECT NOW() AS time", (err, result) => {
    if (err) {
      return res.send("DB Error");
    }
    res.send(`Server Time: ${result[0].time}`);
  });
});

// Start server
app.listen(3000, () => {
  console.log("Server running on port 3000");
});

# 🛢️ 3. MySQL Commands (RDS)

   Connect to RDS
   mysql -h your-rds-endpoint -u admin -p
   
   Create database & table
   
   CREATE DATABASE testdb;
   USE testdb;

  CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50),
    email VARCHAR(100)
   );
Insert data (Replication Test)
INSERT INTO users (name, email)
VALUES ("Om", "om@gmail.com");

# 🔁 4. Test Replication (DR Region) 

  Run same query in Read Replica
  SELECT * FROM users;

# ⚡ 5. Failover Steps
        1.Go to AWS RDS
        2.Select Read Replica
        3.Click Promote
        
        Update endpoint in app.js
        -"new-dr-endpoint"

# 🖥️ 6. Run Application
       node app.js

      -Open browser:
       http://localhost:3000

# ☁️ 7. EC2 Setup Commands

Connect to EC2
ssh -i your-key.pem ec2-user@your-ec2-ip

Install Node.js
sudo yum update -y
curl -fsSL https://rpm.nodesource.com/setup_18.x | sudo bash -
sudo yum install -y nodejs

Upload project to EC2
scp -i your-key.pem -r dr-project ec2-user@your-ec2-ip:/home/ec2-user/

Run app on EC2
cd dr-project
npm install
node app.js

# 🐙 8. GitHub Upload Commands

git init
git add .
git commit -m "DR project"

git branch -M main
git remote add origin https://github.com/your-username/project-name.git
git push -u origin main

# ✅ Final Flow

  EC2 → Node.js App
  App → Primary RDS
  RDS → DR Replica
  Fail → Promote DR → Update endpoint
 
# 📸 Important screenshots

1️⃣ “AWS RDS Database Setup (Primary & DR Replica)”
   <img width="1919" height="1079" alt="Image" src="https://github.com/user-attachments/assets/bfd7b8ee-2b90-4436-a14e-37d0323989b4" />
 
2️⃣ “Application Running on EC2 Instance (Primary Region)”
   <img width="1919" height="1079" alt="Image" src="https://github.com/user-attachments/assets/776e519a-5bf2-47ce-8e34-ff5939bd5760" />

3️⃣ “Database Connectivity and Data Retrieval from RDS”
  <img width="1919" height="1079" alt="Image" src="https://github.com/user-attachments/assets/137bbf2e-5771-4a2c-b861-8b77f669d902" />

4️⃣ “EC2 Instance Deployment (Application Server)”
   <img width="1919" height="1079" alt="Image" src="https://github.com/user-attachments/assets/8458dd7e-bfb3-4f91-a3a7-b6fde9ce336f" />

5️⃣ “Amazon S3 Bucket for Storage / Backup”
   <img width="1915" height="1079" alt="Image" src="https://github.com/user-attachments/assets/78061a39-fe96-4460-9062-ee7eba9b0615" />

6️⃣ “Application Running After Failover (DR Region)”
   <img width="1919" height="1079" alt="Image" src="https://github.com/user-attachments/assets/1a368540-c17e-4fe5-a179-f64fddd19f20" />


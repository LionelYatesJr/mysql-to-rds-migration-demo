# MySQL → AWS RDS Migration Demo

🎯 Objective
Migrate a local MySQL database (company_db) to AWS RDS (Free Tier), showcasing a cloud-native database modernization.

🛠 Requirements
- Local MySQL installation (e.g., via Homebrew on macOS)
- AWS account with RDS MySQL instance (Free Tier)
- mysqldump and mysql CLI tools
- IAM permissions and security group allowing remote access to RDS

🔧 Key Commands

# 1. Export local DB
mysqldump -u root -p \
  --databases company_db \
  --single-transaction \
  --no-tablespaces \
  --set-gtid-purged=OFF \
  > company_db.sql

# 2. Import into AWS RDS
mysql -h <RDS_ENDPOINT> -P 3306 -u admin -p < company_db.sql

✅ Outcome
- Successfully migrated company_db with all schema and data intact into AWS RDS
- Verified via SQL queries on RDS:
  SHOW DATABASES;
  USE company_db;
  SELECT * FROM employees;
- Demonstrates a repeatable process for data modernization and AWS RDS proficiency

📄 Supporting Files
- MySQL_to_RDS_Tutorial_with_Brew.pdf — full walkthrough PDF
- screenshots/local_mysql_setup.png — local DB setup
- screenshots/rds_verification.png — RDS query verification



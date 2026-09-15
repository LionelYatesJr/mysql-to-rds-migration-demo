# MySQL to AWS RDS Migration Demo

A database modernization project that migrates a local MySQL database into **Amazon RDS for MySQL** using standard MySQL export/import tooling.

The goal was to practice a repeatable migration workflow while demonstrating hands-on experience with AWS database services, connectivity, security groups, and data validation.

## Project Objective

Migrate a local MySQL database named `company_db` to Amazon RDS while preserving the database schema and data.

## Tech Stack

- MySQL
- Amazon RDS for MySQL
- AWS Security Groups
- `mysqldump`
- MySQL CLI
- macOS / Homebrew

## Migration Workflow

```text
Local MySQL Database
        |
     mysqldump
        |
   SQL Backup File
        |
     mysql CLI
        |
Amazon RDS for MySQL
        |
 Validation Queries
```

## Requirements

- Local MySQL installation
- AWS account
- Amazon RDS MySQL instance
- `mysqldump` and `mysql` CLI tools
- Network access to the RDS instance
- Security-group rules configured for the required MySQL connection

## Migration Steps

### 1. Export the local database

```bash
mysqldump -u root -p \
  --databases company_db \
  --single-transaction \
  --no-tablespaces \
  --set-gtid-purged=OFF \
  > company_db.sql
```

### 2. Import the dump into Amazon RDS

```bash
mysql -h <RDS_ENDPOINT> -P 3306 -u admin -p < company_db.sql
```

> Credentials and database endpoints should be kept out of source control.

### 3. Validate the migration

Example verification queries:

```sql
SHOW DATABASES;
USE company_db;
SELECT * FROM employees;
```

## Outcome

- Migrated `company_db` from a local MySQL environment to Amazon RDS
- Preserved database schema and data
- Verified the migrated database through SQL queries
- Practiced RDS connectivity and security-group configuration
- Created a repeatable migration process that can be adapted to similar database modernization tasks

## Supporting Material

The repository also includes supporting documentation and screenshots from the migration process, including:

- `MySQL_to_RDS_Tutorial_with_Brew.pdf`
- `screenshots/local_mysql_setup.png`
- `screenshots/rds_verification.png`

## Skills Demonstrated

- MySQL backup and restore workflows
- Amazon RDS provisioning and connectivity
- Database migration validation
- AWS networking and security-group fundamentals
- CLI-based cloud operations
- Technical documentation

## Author

**Lionel Yates Jr.**  
Cloud / DevOps projects: [GitHub Profile](https://github.com/LionelYatesJr)  
CloudWorks: [lyatescloudworks.com](https://lyatescloudworks.com)

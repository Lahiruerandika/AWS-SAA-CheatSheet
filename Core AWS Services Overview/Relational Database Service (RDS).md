## AWS RDS - Relational Database Service (RDS)

- It is a managed database service for relational databases
- It allows us to create databases in the cloud that are managed by AWS
- RDS offerings provided by AWS:
    - PostgreSQL
    - MySQL
    - MariaDB
    - Oracle
    - Microsoft SQL Server
    - Aurora
- Advantages of AWS RDS over deploying a relational database on EC2:
    - RDS is a managed service, meaning:
        - Automated provisioning, OS patching
        - Continuous backups and restore to specific timestamp (Point in Time Restore)
        - Monitoring dashboards
        - Read replicas
        - Multi AZ setup
        - Maintenance windows for upgrades
        - Scaling capability (vertical and horizontal)
        - Storage backed by EBS (GP2 or IO)
- Disadvantages:
    - No SSH into the instance which hosts the database

## RDS Backups

- Backups are automatically enabled in RDS
- AWS RDS provides automated backups:
    - Daily full backup of the database (during the maintenance window)
    - Transaction logs are backed up by RDS every 5 minutes, providing the ability to do point-in-time restores
    - There is a 7-day retention for the backups which can be increased to 35 days
- DB Snapshots:
    - These are manually triggered backups by the users
    - Retention can be as long as the user wants
    - Helpful for retaining the state of the database for a longer period of time


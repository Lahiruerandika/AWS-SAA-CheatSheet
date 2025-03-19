# AWS DataSync

- Can be used to move large amount of data from on-premise to AWS
- Ability to synchronize to S3, EFS, FSx for Windows
- Ability to move data from NAS of file system to NFS or SMB
- Replication tasks can be scheduled hourly, daily or weekly
- We can leverage the DataSync agent to connect to our systems

## Transferring large amount of data to AWS

- Problem: transfer 200TB of data in the cloud with a 100 Mbps internet connection.
- Solutions:
    - Over the internet / Site-to-Site VPN:
        - Immediate to setup
        - It will take approximately 185 days

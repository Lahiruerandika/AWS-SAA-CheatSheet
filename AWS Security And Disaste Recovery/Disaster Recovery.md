# Disaster Recovery

- Disaster: any event that has a negative impact on a company's business continuity or finances
- Disaster Recovery (DR) is about preparing for and recovering from a disaster
- Disaster recovery solutions:
    - On-premise to on-premise: traditional DR, expensive
    - On-premise to cloud: hybrid recovery
    - AWS Cloud Region A to AWS Cloud Region B

## RPO and RTO

- RPO - Recovery Point Objective: How often we create backups. Time between the RPO and the disaster is the data loss
- RTO - Recovery Time Objective: The point in time when the recovery finishes. The time between the disaster and the RTO is downtime

## Disaster Recovery Strategies

- Backup and Restore: high RPO, cheap, easy to manage and accomplish
- Pilot Light:
    - A small version of the app is always running in the cloud
    - Useful for critical core (pilot light)
    - Similar to backup and restore strategy
    - Faster than backup and restore as critical system are already running
- Warm Standby
    - Full system is up and running but at a minimal size
    - Upon disaster we can scale to production load
- Hot Site / Multi Site Approach
    - Very low RTO - very expensive
    - Full production scale is running on the cloud
- All AWS Multi Region

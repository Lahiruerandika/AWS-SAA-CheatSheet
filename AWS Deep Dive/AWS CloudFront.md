# AWS CloudFront

- CloudFront is a content delivery network (CDN).
- It improves read performance; content is cached at edge locations (currently there are 216 edge locations globally).
- CloudFront also offers DDoS protection, integration with Shield, and integration with AWS WAF (Web Application Firewall).
- CloudFront allows exposing external HTTPS endpoints and can also communicate with internal HTTPS backends.

## CloudFront Origins

- The location of the data distributed by CloudFront can be:
    - **S3 bucket:**
        - Recommended for distributing files and caching them at edge locations.
        - Offers enhanced security with CloudFront **Origin Access Identity (OAI)**.
        - CloudFront can be used as an ingress for uploading files to S3.
    - **Custom Origin (HTTP),** which could be:
        - Application Load Balancer
        - EC2 instance
        - S3 website (must enable the static website functionality on the bucket)
        - Any other HTTP backend

## CloudFront Geo Restriction

- CloudFront can restrict access to the distribution based on geographic location.
- It provides:
    - **Whitelisting:** Allows users to access the content if they are from countries on the approved list.
    - **Blacklisting:** Denies access for users from countries listed on the banned list.
- The country is determined using a third-party Geo-IP database.
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

## CloudFront vs. S3 Cross-Region Replication

- **CloudFront:**
    - Global Edge network.
    - Files are cached for a time period (TTL).
    - Recommended for static content that must be available worldwide.
- **S3 Cross-Region Replication:**
    - Must be configured for each region where replication is required.
    - Files are updated in near real-time.
    - Read-only.
    - Recommended for dynamic content that needs low-latency availability in specific regions.

## CloudFront Signed URL/Signed Cookies

- Used for distributing exclusive content to specific users.
- When a signed cookie/URL is created, a policy needs to be attached, which should contain:
    - URL expiration date.
    - IP ranges that can access the data.
    - Trusted signers (AWS accounts allowed to create a signed URL).
- **Signed URL time-to-live:**
    - For shared content (movies, music), the TTL should be short.
    - For private content, the TTL can be longer.
- **Signed URL:** Grants access to individual files.
- **Signed Cookies:** Grants access to multiple files.

## CloudFront Signed URL vs. S3 Pre-Signed URL

- **CloudFront Signed URL:**
    - Allows access to a path, regardless of the origin.
    - Uses an account-wide key pair; only the root account can manage it.
    - Can filter by IP, path, date, and expiration.
    - Leverages all CloudFront caching features.
- **S3 Pre-Signed URL:**
    - Issues requests as the user who pre-signed the URL.
    - Uses the IAM key of the signing IAM principal.
    - Has a limited lifetime.
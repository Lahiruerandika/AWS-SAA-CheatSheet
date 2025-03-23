# AWS WAF - Web Application Firewall

- Protects web applications from common web exploits (Layer 7)
- WAF can be deployed on Application Load Balancer, API Gateway and CloudFront
- To use WAF we need to define a Web Access Control List (ACL):
    - Rules can include: IP addresses, HTTP headers, HTTP body or URI strings
    - Protects from common attacks such as SQL injection and Cross-Site Scripting (XSS)
    - Size constraint
    - Geo-match, block certain countries
    - Rate-based rules, for DDoS protection

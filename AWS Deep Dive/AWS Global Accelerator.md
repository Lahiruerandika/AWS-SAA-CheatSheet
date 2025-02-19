# AWS Global Accelerator

## Unicast IP vs Anycast IP

- **Unicast IP**: A single server holds one IP address.
- **Anycast IP**: Multiple servers share the same IP address, and the client is routed to the nearest one.

## AWS Global Accelerator 

- It leverages the **AWS internal network** to route traffic to applications.
- **Two Anycast IPs** are created for the application, which are **global**. Traffic from these IPs is sent to **Edge Locations**, which then forward it to the application using the **AWS global network**.
- **Global Accelerator works with**:
    - Elastic IP
    - EC2 instances
    - ALB (Application Load Balancer)
    - NLB (Network Load Balancer)  
    These can be either **public** or **private**.
- **Provides consistent performance by**:
    - **Intelligent routing** to the lowest latency endpoint and **fast regional failover**.
    - **Bypassing client-side caching**, as the **IP address remains static**.
    - Keeping traffic **internal to the AWS network**.

### Health Checks

- **Global Accelerator continuously performs health checks** on application endpoints.
- **Failover occurs in less than 1 minute** if an instance becomes unhealthy.
- **Ideal for disaster recovery** scenarios.

### Security

- **Provides 2 external IPs**, which may need to be **whitelisted**.
- **DDoS protection** is included through **AWS Shield**.

## AWS Global Accelerator vs. CloudFront

- **Both services use the AWS global network and edge locations** worldwide.
- **Both integrate with AWS Shield for DDoS protection**.

### **CloudFront**

- **Improves performance** for both:
    - **Cacheable content** (e.g., images, videos).
    - **Dynamic content** (e.g., API acceleration, dynamic site delivery).
- **Content is served directly from Edge Locations**.

### **Global Accelerator**

- **Improves performance** for a wide range of applications over TCP or UDP**.
- **Traffic is proxied from Edge Locations** to the application backend.
- **Best suited for non-HTTP applications**, such as:
    - **Gaming (UDP)**.
    - **IoT (MQTT)**.
    - **Voice over IP (VoIP)**.
- **Can also be used for HTTP applications** when:
    - **Static IP addresses** are required.
    - **Fast regional failover** is essential.

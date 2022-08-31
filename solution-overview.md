# Solution Overview

# Environments
    
We will have below environments 

| Environment | Description |
| ----------- | ----------- |
| DEV         | Developer environment for initial dev test.  |
| UAT         | Like to Like version of Production. This will be used for integration, User Acceptance Test and debugging critical PROD issues        |
| PROD        | Production Environment with no direct access to update bucket    |





We can setup Infrastructure and CI/CD for the requirement in 2 ways depending on if we can use lambda's or not. 
Lambda's has below restriction 
- Maximum memory : 10,240 MB
- Maximum CPU : 6 CPU
- Maximum Duration : 15 min


Below are the resources we will be using in both the solutions 
## Storage
### S3 
    - The most highly available service of AWS
    - Private buckets with SSE-S3 encryption enabled
    - Access allowed via bucket policy
    - Accessible via VPC endpoint for application processing
    - Accessible to Cloudfront via Origin Access Identity (OAI)
    
## Delivery
### Cloudfront

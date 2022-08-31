# Solution Overview

# Environments
    
We will have below environments 

| Environment | Description |
| ----------- | ----------- |
| DEV         | Developer environment for initial dev test.  |
| UAT         | Like to Like version of Production. This will be used for integration, User Acceptance Test and debugging critical PROD issues        |
| PROD        | Production Environment with no direct access to update bucket    |


## Storage
### S3 
    - The most highly available service of AWS
    - Private buckets with SSE-S3 encryption enabled
    - Access allowed via bucket policy
    - Accessible via VPC endpoint for application processing
    - Accessible to Cloudfront via Origin Access Identity (OAI)
    
## Delivery
### Cloudfront
    - Cloudfront will be used to deliver all the static content including css, js and images
    - We will deliver the final generated image to user using cloudfront.
    - We will cache the static content in cloudfront as required depending on usage and image change frequency. As higher invalidations can increase cost.


## Security 
### WAF (Web Application firewall)
    - This will be added in front of Cloudfront and load balancer to prevent any malicious calls.
    - We can use rate limiting from particular IP using WAF as well.

## Application 

We can setup Infrastructure and CI/CD for the requirement in 2 ways depending on if we can use lambda's or not. 

Lambda's has below restriction
- Maximum memory : 10,240 MB
- Maximum CPU : 6 CPU
- Maximum Duration : 15 min
- Maximum concurrent execution (can be increased) - 1000 / region


### Solution 1 
### Solution 2

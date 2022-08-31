# Solution Overview

# Environments
    
We will have below environments 

| Environment | Description |
| ----------- | ----------- |
| DEV         | Developer environment for initial dev test.  |
| UAT         |- Like to Like version of Production. 
               -This will be used for integration, User Acceptance Test and debugging critical PROD issues        |
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
- As content is delivered using AWS Edge locations the delivery will be without latency issues.
- We can customize the caching time for each path pattern, as a whole etc.
- We will cache the static content in cloudfront as required depending on usage and image change frequency. As higher invalidations can increase cost.
- AWS is responsible for DDoS prevention on Cloudfront.


## Security 
### WAF (Web Application firewall)
- This will be added in front of Cloudfront and load balancer to prevent any malicious calls.
- We can use rate limiting from particular IP using WAF as well.

### Other security considerations 
- The application will be hosted in private subnet
- Access to other AWS services will be via IAM roles
- API gateway will be private to be available within VPC 


## Caching
### Redis
- Redis is in-memory data structure store which provides faster delivery of cached items. 
- AWS Redis also support autoscaling if the resource requirement increases. 
- Redis supports snapshots for easy recovery of older data.
- Redis to store the link for processed images for easy delivery of similar combinations. 
- Redis also can be used for rendered HTML pages for frontend.
    
## Application Hosting

We can setup Infrastructure and CI/CD for the requirement in 2 ways depending on if we can use lambda's or not. 

Lambda's has below restriction
- Maximum memory : 10,240 MB
- Maximum CPU : 6 CPU
- Maximum Duration : 15 min
- Maximum concurrent execution (can be increased) - 1000 / region


### Solution 1 - Preferred
This solution will host Frontend application in ECS Fargate and the REST APIs in AWS lambda.

With AWS lambda and ECS Fargate we do not have to manage the hosting server and can easily configure them as per requirement.

Architecture Diag : [Solution 1](../solution-1 "Solution 1")
CICD Pipeline : [CICD](../cicd-solution-1 "Solution 1")

### Solution 2
This solution will host the frontend application and backend REST APIs in kuberntes using AWS EKS fargate.

Architecture Diag : [Solution 2](../solution-2 "Solution 2")
CICD Pipeline : [CICD](../cicd-solution-2 "Solution 1")


## DR


## Cost

# Solution Overview

- Considering microservice approach for application to seperate out Frontend and  backend functionality into smaller modular applications.
- This will also help in managing lifecycle of each functionality separately.
- Testing can easily be performed on each functinality separately.


# Environments
    
We will have below environments 

| Environment | Description |
| ----------- | ----------- |
| DEV         | Developer environment for initial dev test.  |
| UAT         |Like to Like version of Production. <br> This will be used for Automation, User Acceptance Test and debugging critical PROD issues        |
| PROD        | Production Environment with no direct access to update bucket    |

- Each environment will have its own branch as below

| Environment | Branch      |
| ----------- | ----------- |
| DEV         | dev         |
| UAT         | uat/pre-prod |
| PROD        | main/master |

- feature branches to be created from master and merged to dev for development environment
- create release branch from master and merge feature branches ready to be moved to higher env. Merge release branch to UAT branch.
- Once testing is completed in UAT merge the release branch to master and rebase merge UAT and DEV branches from master.
- This will keep master as source of truth for PRODUCTION.

## Storage
### S3
- S3 will host all the images of cat and hat along with the processed images.
- It is most highly available service of AWS.
- Private buckets with SSE-S3 encryption enabled.
- We will enable versioning on our bucket to keep previous image version and can delete them using lifecycle policy after certain amount of time.
- Access allowed via bucket policy.
- Accessible via VPC endpoint for application processing.
- Accessible to Cloudfront via Origin Access Identity (OAI).
    
## Delivery
### Cloudfront
- Cloudfront will be used to deliver all the static content including css, js and images.
- We will deliver the final generated image to user using cloudfront.
- As content is delivered using AWS Edge locations the delivery will be without latency issues.
- We can customize the caching time for each path pattern, as a whole etc.
- We will cache the static content in cloudfront as required depending on usage and image change frequency. As higher invalidations can increase cost.
- AWS is responsible for DDoS prevention on Cloudfront.


## Security 
### WAF (Web Application firewall)
- This will be added in front of Cloudfront and load balancer to prevent any malicious calls.
- We can use rate limiting from particular IP using WAF as well.
- We cab use AWS pre defined rules along with custom rules to prevent attacks on our application.

### Other security considerations 
- The application will be hosted in private subnet.
- Access to other AWS services will be via IAM roles.
- API gateway will be private to be available within VPC. 
- API gateway will have secret key for diff env and user.
- We can have seperate environment within API Gateway for better testing.


## Caching
### Redis
- Redis is in-memory data structure store which provides faster delivery of cached items. 
- AWS Redis also support autoscaling if the resource requirement increases. 
- Redis supports snapshots for easy recovery of older data.
- Redis to store the link for processed images for easy delivery of similar combinations. 
- Redis also can be used for rendered HTML pages for frontend.

## Queue
### SQS
- This will be used to handle scenario where multiple request are for same image combinations.
- If there are multiple users requesting same combination not all will have to go through processing of image. 


## Application Hosting

- We can setup Infrastructure and CI/CD for the requirement in 2 ways depending on if we can use lambda's or not. 

Lambda's has below restriction
- Maximum memory : 10,240 MB
- Maximum CPU : 6 CPU
- Maximum Duration : 15 min
- Maximum concurrent execution (can be increased) - 1000 / region
- Languages : It doesn't support languages like PHP, React etc. at the moment 


### Solution 1 - Preferred
- This solution will host Frontend application in ECS Fargate and the REST APIs in AWS lambda.
- With AWS lambda and ECS Fargate we do not have to manage the hosting server and can easily configure them as per requirement.
- This solution will not incurr cost for hosting backend solution as lambda only inccurs cost when it is triggered and based on mem and cpu used. 
- ECS, Redis, ALB, lambda and API gateway will be spread across Availability Zones in Highly available infrastructure. 

Architecture & CICD : [Solution 1](../solution-1 "Solution 1")


### Solution 2
- This solution will host the frontend application and backend REST APIs in kuberntes using AWS EKS fargate.
- This solution will incurr daily cost of hosting backend solution in eks pods.
- The cost to use ECR for backend application is more compared to storage cost in S3. 
- EKS, Redis, ALB and API gateway will be spread across Availability Zones in Highly available infrastructure.

Architecture & CICD : [Solution 2](../solution-2 "Solution 2")

## Monitoring and Alerting
- CLoudwatch will be used to store all the logs. 
- Cloudwatch insights will be used for performance monitoring
- Cloudwatch alarms will be used for alerting
- 
## DR

In case of 1 region failing completely. We can follow below approach for DR
- Use Global Accelerator in front of external load balancer with all the traffic going to main region.
- Sync docker images  to DR region
- S3 bucket replication to DR region. 
- Sync redis cache backup to DR region
- Setup basic infrastructure in another region. To prevent costing we can stop running any ECS container and disable cloudfront in DR region.


## Cost saving
- To save cost we can turn off ECS/EKS, disable cloudfront in lower environment. 
- Using lifecycle policy to remove processed image which are not used for longer time.
- keeping docker image size to small. 

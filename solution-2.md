# Solution 2 Architecture
- AWS EKS to host the frontend application and REST APIs 
- AWS EKS takes care of control plane management
- ALB will deliver the frontend of application
- All the images, css, js will be delivered via Cloudfront
- API gateway will be used to deliver REST APIs to Frontend application
- VPC endpoint to connect to S3 from lambda or ECS
- API gateway can cache the response for calls


![solution-2](../Solution-Solution 2.jpg)!


# Solution 2 CICD

![CICD-2](../Solution-CICD - SOLUTION 2.jpg)!

# Solution 1 
## Architecture
- ECS will host the frontend application available to end user
- ALB will deliver the frontend of application
- All the images, css, js will be delivered via Cloudfront
- The application will trigger lambda for processing images, Fetching existing image link using API Gateway
- VPC endpoint to connect to S3 from lambda or ECS
- API gateway can cache the response for calls

![solution-1](../Solution-Solution 1.jpg)


## CICD
![CICD](../Solution-CICD - SOLUTION 1.jpg)

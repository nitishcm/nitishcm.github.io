# Solution 1 
## Architecture
- ECS will host the frontend application available to end user
- ALB will deliver the frontend of application
- All the images, css, js will be delivered via Cloudfront
- The application will trigger lambda for processing images, Fetching existing image link using API Gateway
- VPC endpoint to connect to S3 from lambda or ECS
- API gateway can cache the response for calls
- SQS queue to manage the request queue for image processing

![solution-1](../Solution_1.jpeg)


## CICD
![CICD](../CICD-SOLUTION_1.jpeg)


[HOME](../solution-overview )

# Environment

| Environment      | Description |
| ----------- | ----------- |
| DEV         | Developer environment for initial dev test.  |
| UAT         | Like to Like version of Production. This will be used for integration, User Acceptance Test and debugging critical PROD issues        |
| PROD        | Production Environment with no direct access to update bucket    |


# AWS Resources to use
## Storage
### S3 
    - The most highly available service of AWS
    - Private buckets with SSE-S3 encryption enabled
    - Access allowed via bucket policy
    - Accessible via VPC endpoint for application processing
    - Accessible to Cloudfront via Origin Access Identity (OAI)
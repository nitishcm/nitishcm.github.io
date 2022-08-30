#Environment

DEV - Trimmed down version of prod
Pre Prod/UAT - Like to Like of Production
Prod 

<ul>
    <li>Image storage : S3  </li>
    Image delivery : Cloudfront
    Security : WAF
    Caching - Redis 
    
</ul>
<h2>Scenario 1</h2>
<p>The web frontend and image processing both happening as 1 application</p>
<ul>
    <li>The application is running as one for frontend and image processing</li>
Application hosted in ECS with autoscaling based on CPU and Mem 
The load balancer will be used to deliver the web frontend

</ul>
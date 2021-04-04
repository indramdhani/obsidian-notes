# AWS S3 Gateway Endpoint to Save Bandwith
## VPC Endpoint

-   Go to vpc dashboard and select Endpoint submenu [](https://ap-southeast-1.console.aws.amazon.com/vpc/home?region=ap-southeast-1#Endpoints:sort=vpcEndpointId)[https://ap-southeast-1.console.aws.amazon.com/vpc/home?region=ap-southeast-1#Endpoints:sort=vpcEndpointId](https://ap-southeast-1.console.aws.amazon.com/vpc/home?region=ap-southeast-1#Endpoints:sort=vpcEndpointId)
-   Create new endpoint here
    -   select S3 service with Gateway as a type
    -   select the VPC as the source
    -   (optional) add respective tags

## AWS S3 Endpoint

-   Go to AWS dashboard and select the Access Points submenu
-   Create access point here
    -   fill the access point name
    -   select the bucket that will use the endpoint
    -   choose VPC as the network origin ( it will make the S3 endpoint only able to be used from the VPC / intranet )
        -   fill in the VPC ID

## Accessing S3 Bucket using the endpoint

-   use the endpoint ARN to access the bucket `arn:aws:s3:aws-region:account-id:accesspoint/access-point-name`
-   since we choose VPC as the network origin, the bucket will be accessible only from EC2 instance that use same VPC. it will reduce the cost since it never leave AWS network

#aws #s3 #gateway
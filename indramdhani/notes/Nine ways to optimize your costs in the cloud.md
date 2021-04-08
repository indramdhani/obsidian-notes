# Nine ways to optimize your costs in the cloud

-   **stop idle/non critical/production ec2 & rds → AWS Instance scheduler**
-   use arm based ec2 instances → AWS Graviton
-   chose amazon ec2 spot for fault tolerant workload, stateless, loosely coupled
-   **use ec2 resource optimisation in aws cost explorer and rightsize the instance**
-   **use s3 lifecycle configuration rules, move the object to lower class. use it if the access has default access pattern**
-   **enable s3 intelligent tiering, use it for bucket with unknown access pattern**
-   **use amazon s3 gateway endpoint, communicate with s3 on private network. use it for non public bucket**
-   use on demand capacity mode for dynamodb
-   use compute saving plans, 1 year no upfront compute saving plans

#aws #cost-optimization #ec2 #rds #s3 #ondemand #dynamodb #saving-plans
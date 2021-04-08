# Increase efficiency of your Backup and Recovery workflow with AWS
-   minimize data loss ( recovery point objective )
-   minimize time to recover - recover time objective
-   balancing cost with liability ( of losing data )
-   initial question to answer
    -   how critical the app to the bussines
    -   how are you storing the data
-   use cloud native workload → **AWS Backup**

backup Storage & service:

-   object storage → AWS S3 / Glacier / Glacier Deep Archive → store backup data
    -   transfer method: direct connect / vpn gate / internet
    -   communication to the s3: native s3 integration / api / tape gateway
    -   minimize disk storage
-   block storage
-   file
-   backup
-   data transfer

#aws #backup #recovery #cost-optimization
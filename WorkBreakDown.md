## Direct upload pre-check breakdown 

### step 1: AWS Account and Resource creation
AWS IAM 
AWS s3
AWS Route53
AWS API gateway
AWS SQS
AWS DynomDB
AWS IoT(core, management, ~~defender~~) 
AWS KVS

### step2: No OAUTH direct link upload (port 1883)
1. 📛 mqtt client / Camera ? 
2. AWS create a presigne-url for camera without any authentication with AWS s3 ?
3. mqtt client (put) ----> AWS s3


### step 3: deploy the original `CC BE`, verification the process (port over tls 8883)
1. 📛 CC BE deployment document & implementation 

### step 4: transfer above step to CN 
1. **CC BE need be developed (connect the User with Camera) and to control AWS IOT to create thing/endpoint/pre-signed URL**
   - 📛Sony account (how to ?) 
   - 📛MT service(storage) 
   - 📛How to use Sony Account OAuth to create MT service storage pre-signed URL
2. mqtt client with pre-configured device ID or x509 key (need to be implemented) and authenticated
3. mqtt use the presigned URL to PUT data to Storage 
4. Simple test

### Doc & maunal prepare


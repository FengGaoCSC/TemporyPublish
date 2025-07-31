## 🎥 Work breakdown and Assignment

### 🧩 Development environment
- Python 3.12
- C++ 14
- AWS CN
  - Sony Account
  - Tecent cloud storage service

### 📌 Task 1:
- 🔀 Resource creation 
  - AWS Route53 (❓DNS name need Duan-san provide)
  - ~~AWS API gateway~~
  - ✅ AWS SQS 
  - ~~AWS DynomDB~~
  - ✅ AWS IoT(core, management, ~~defender~~) -> Config/Get the MQtt endpoint  
  - ✅ AWS KVS
- 🔀 Simple Mqtt client(by python authentication on port 8883)
  - **phase1**: 
    - ✅ just can connect to AWS IoT endpoint w/o authentication on port 1883 is OK
    - ✅ verify S3 bucket, Mqtt client could use to put something
    - ✅ verify KVS feature

### 📌 Task 2: (can parall with task 1)
- 🔀 Deploy the system according 器連携PF_デプロイマニュアル.docx
  - If any question or configuration need,(❗ Duan-san could give help)

### 📌 Task 3:
- 🔀 Simple Mqtt client
  - **Phase 2:**
    - 🔴 ✅AWS IoT 如何使用本地证书签发认证的过程: know-how & how to implement.   
    - support PTP to get the pre-signed URL from APP。 
    - ✅ Mqtt client using the pre-signed URL to PUT images by TLS over port：8883（❓here maybe not AWS IoT endpoint since )
    - ❗Mqtt client parameters: Device ID & Key 由 Duan-san 提供
    - ✅ AWS KVS （kenises video stream) verification .
    - 🔴 ✅Mqtt client `put` 后需要publish 一个URL让别人知道（即使用该kvneis list URL可以直接访问该上传资源） 
- 🔀 ❗Pre-signed URL & user with deviceID relationship 
  - Duan-san provide
    - multipart API
    - Singed URL for trailer.mp4,
    - device client using above to direct upload.

### 📌 Task 4:
- 🔀 Final Mqtt client
  - **Implement the following feature into one process**
    - Support PTP to get the pre-signed URL from APP。 
    - Mqtt client using the pre-signed URL to PUT images
    - AWS KVS （kenises video stream) verification .
    - Mqtt client `put` 后需要publish 一个URL让别人知道（即使用该kvneis list URL可以直接访问该上传资源） 
- 🔀 Document
  - AWS configuration manual
  - Mqtt client usage manual
    
 
---

## Appendix:

### 🎥Direct upload pre-check breakdown 

#### 🔀step 1: AWS Account and Resource creation
- ~~AWS IAM~~ 
- ~~AWS s3~~
- AWS Route53
- AWS API gateway
- AWS SQS
- AWS DynomDB
- AWS IoT(core, management, ~~defender~~) 
- AWS KVS

#### 🔀step2: No OAUTH direct link upload (port 1883)
1. 📛 mqtt client / Camera ? 
2. AWS create a presigne-url for camera without any authentication with AWS s3 ?
3. mqtt client (put) ----> AWS s3


#### 🔀step 3: deploy the original `CC BE`, verification the process (port over tls 8883)
1. ~~📛 CC BE deployment document & implementation~~  

#### 🔀step 4: transfer above step to CN 
1. ~~**CC BE need be developed (connect the User with Camera) and to control AWS IOT to create thing/endpoint/pre-signed URL**~~
   - ~~📛Sony account (how to ?)~~ 
   - ~~📛MT service(storage)~~ 
   - ~~📛How to use Sony Account OAuth to create MT service storage pre-signed URL~~
2. mqtt client with pre-configured device ID(Duan-san will give)  or x509 key (need to be implemented) and authenticated
3. mqtt use the presigned URL to PUT data to Storage 
4. Simple test

#### 🔀Doc & maunal prepare

---

### 📌经过和Duan-san的确认：
1。 先开始部署各个IOT 相关的模块（按照机器连携.docx) 看看那一步会有问题， DeviceID Duan-san 会给出
2. WEB app 认证 和 Authentication 是 不用我们关心的， 到时候 会给我们一个Presigned-URL, MQtt Client只要PUT上去就行
   - KVS 验证
   - PUT 验证
   - APP 给到MQTT Client(模拟相机）的需要通过PTP

### Notes & verification 

- 🔴 AWS IoT 如何使用本地证书签发认证的过程: know-how & how to implement. 
```txt
这个今天验证了以下本地签名：
步骤： 
1. 使用openssl 生成root ca
2. 使用 openssl 生成设备名camera001的public key & private key
3. 本地签名
4. AWS console IoT 界面配置多设备选项，并应用相应的policy (我们使用testThing的policy) 选择x509认证并上传第一步本地root ca到AWS IoT core 
5. 使用昨天写的mqtt client 程序, 参数为AWS root ca, device ID, 第2，3步生成的private key和签名，IoT endpint 即可connect AWS IoT.
6. 云端AWS IoT -> things下会自动创建相应的things, name=device name, 该过程全自动， 无需手动配置
```
```txt
S3 pre-signed url tempoary credential
1. create s3 access role
2. create s3 access policy
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws-cn:s3:::test-thing-bucket/${iot:ThingName}/*"
            ]
        }
    ]
}
3. create alias role name and enable assume alias role
4. get the url of the alias role
5. device to get the assumeed alias role credential through the alias role
6. device was under control of this alias role and access policy
```



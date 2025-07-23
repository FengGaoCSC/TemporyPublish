## 🎥Direct upload pre-check breakdown 

### 🔀step 1: AWS Account and Resource creation
- ~~AWS IAM~~ 
- ~~AWS s3~~
- AWS Route53
- AWS API gateway
- AWS SQS
- AWS DynomDB
- AWS IoT(core, management, ~~defender~~) 
- AWS KVS

### 🔀step2: No OAUTH direct link upload (port 1883)
1. 📛 mqtt client / Camera ? 
2. AWS create a presigne-url for camera without any authentication with AWS s3 ?
3. mqtt client (put) ----> AWS s3


### 🔀step 3: deploy the original `CC BE`, verification the process (port over tls 8883)
1. ~~📛 CC BE deployment document & implementation~~  

### 🔀step 4: transfer above step to CN 
1. ~~**CC BE need be developed (connect the User with Camera) and to control AWS IOT to create thing/endpoint/pre-signed URL**~~
   - ~~📛Sony account (how to ?)~~ 
   - ~~📛MT service(storage)~~ 
   - ~~📛How to use Sony Account OAuth to create MT service storage pre-signed URL~~
2. mqtt client with pre-configured device ID(Duan-san will give)  or x509 key (need to be implemented) and authenticated
3. mqtt use the presigned URL to PUT data to Storage 
4. Simple test

### 🔀Doc & maunal prepare

---

## 📌经过和Duan-san的确认：
1。 先开始部署各个IOT 相关的模块（按照机器连携.docx) 看看那一步会有问题， DeviceID Duan-san 会给出
2. WEB app 认证 和 Authentication 是 不用我们关心的， 到时候 会给我们一个Presigned-URL, MQtt Client只要PUT上去就行
   - KVS 验证
   - PUT 验证
   - APP 给到MQTT Client(模拟相机）的需要通过PTP 



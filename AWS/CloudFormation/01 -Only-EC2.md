# 01 - Only-EC2

## Doc
* [AWS::EC2::Instance](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-ec2-instance.html#aws-properties-ec2-instance--examples)

## Switchs (optional)
1. SecurityGroupIds [List String]
````yaml
SecurityGroupIds: 
- sg-0128a5747c0dbf703
````
2. KeyName
````yaml
KeyName: Ec2-Ama-ca-central
````
   * can have an error (i.g key don't exist even you can see it in console & used !)

---

## SRC
````yaml
---
Resources:
  EC2:
    Type: AWS::EC2::Instance
    Properties:
      AvailabilityZone: ca-central-1a
      ImageId: ami-0c2f25c1f66a1ff4d
      InstanceType: t2.micro
````

### Events
[<img src="https://i.imgur.com/HcEJ5pI.png">](https://i.imgur.com/HcEJ5pI.png)

### S3
[<img src="https://i.imgur.com/VdTcWMW.png">](https://i.imgur.com/VdTcWMW.png)

* SSE-S3
    * AES-256
    
[<img src="https://i.imgur.com/93U1s7W.png">](https://i.imgur.com/93U1s7W.png)


### EC2
[<img src="https://i.imgur.com/ExVVnQJ.png">](https://i.imgur.com/ExVVnQJ.png)

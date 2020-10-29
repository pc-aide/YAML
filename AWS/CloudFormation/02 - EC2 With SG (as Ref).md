# 02 - EC2 With SG (as Ref)

## Doc
* [AWS::EC2::SecurityGroup](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-ec2-security-group.html#aws-properties-ec2-security-group--examples)

## Switchs (optional)
1. 

---

## SRC
````yaml
Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      AvailabilityZone: ca-central-1a
      ImageId: ami-0c2f25c1f66a1ff4d
      InstanceType: t2.micro
      SecurityGroups:
        - Ref: SSHSecurityGroup

  # our EC2 security group
  SSHSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: SSH-IN-MyIP
      SecurityGroupIngress:
      - CidrIp: 0.0.0.0/0
        FromPort: 22
        IpProtocol: tcp
        ToPort: 22
````

### CloudFormation
* Resources 
    * SG: SSH-In-MyIP with random GroupName
    
[<img src="https://i.imgur.com/V5hICVi.png">](https://i.imgur.com/V5hICVi.png)

### EC2
* SG: 

[<img src="https://i.imgur.com/TCsO77X.png">](https://i.imgur.com/TCsO77X.png)
[<img src="https://i.imgur.com/RzkzLTL.png">](https://i.imgur.com/RzkzLTL.png)

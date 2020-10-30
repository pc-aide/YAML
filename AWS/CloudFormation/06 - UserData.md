# 06 - UserData

## Switchs (optional)
1. 

---

## Examples
### 01 - Web SRV
````yaml
Mappings:
    RegionMap:
        us-east-1:
            "AMI": "ami-0947d2ba12ee1ff75"
        ca-central-1:
            "AMI": "ami-0c2f25c1f66a1ff4d"

Parameters:
  KeyPairs:
    Description: Name of existing EC2 KeyPairs
    Type: AWS::EC2::KeyPair::KeyName

Resources:
  EC2:
    Type: AWS::EC2::Instance
    Properties:
      KeyName: !Ref KeyPairs
      # FindInMap = CloudFormation console - not aws configure get region
      ImageId: !FindInMap [RegionMap, !Ref "AWS::Region", AMI]
      InstanceType: t2.micro
      SecurityGroups:
        - !Ref SSHSG
        - !Ref HTTPSG
      #UserData - WebSRV
      UserData:
        Fn::Base64: !Sub |
         #!/bin/bash -xe
         yum update -y aws-cfn-bootstrap
         yum install -y httpd
         systemctl start httpd
         systemctl enable httpd
         echo "<h1>This is a test</h1>" > /var/www/html/index.html
         echo "Hostname: " >> /var/www/html/index.html
         echo "<p style=color:red>$(hostname -f)</p>" >> /var/www/html/index.html
         EC2_AZ=$(curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone)
         echo "<p>In AZ:</p>" >> /var/www/html/index.html
         echo "<p style=color:green>In $EC2_AZ</p>" >> /var/www/html/index.html
         systemctl reload httpd

  # SSH-SG
  SSHSG:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: SSH-IN-MyIP
      SecurityGroupIngress:
      - CidrIp: 61.60.12.4/32
        FromPort: 22
        IpProtocol: tcp
        ToPort: 22

# HTTP-SG
  HTTPSG:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: HTTP-IN-Any
      SecurityGroupIngress:
      - CidrIp: 0.0.0.0/0
        FromPort: 80
        IpProtocol: tcp
        ToPort: 80
````

### Browswer
[<img src="https://i.imgur.com/eLKTG8y.png">](https://i.imgur.com/eLKTG8y.png)

### EC2
[<img src="https://i.imgur.com/zdD1wFh.png">](https://i.imgur.com/zdD1wFh.png)

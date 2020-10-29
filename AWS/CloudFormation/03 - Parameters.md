# 03 - Parameters

## Doc

## Note
* By default - no order, so can put the `parameter` to the top or bottom

## Siwtchs (optional)

---

## Examples
### 01 - SGDecription
````yaml
Parameters:
  SecurityGroupDescription:
    Description: Security Group Description
    Type: String

Resources:
  EC2:
    Type: AWS::EC2::Instance
    Properties:
      AvailabilityZone: ca-central-1a
      ImageId: ami-0c2f25c1f66a1ff4d
      InstanceType: t2.micro
      SecurityGroups:
        - !Ref SSHSG

  # SSH-SG
  SSHSG:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: !Ref SecurityGroupDescription
      SecurityGroupIngress:
      - CidrIp: 0.0.0.0/0
        FromPort: 22
        IpProtocol: tcp
        ToPort: 22
````

---

### 02 - KeyPairs
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

  # SSH-SG
  SSHSG:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: SSH-IN-MyIP
      SecurityGroupIngress:
      - CidrIp: 0.0.0.0/0
        FromPort: 22
        IpProtocol: tcp
        ToPort: 22
````

## Input param
* list of keys:

[<img src="https://i.imgur.com/ZfAqVCT.png">](https://i.imgur.com/ZfAqVCT.png)


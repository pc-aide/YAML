# 04 Mapping

## Notes
* stack Name can be the same if stacks aren't commuting

## Switchs (optional)
1. 

---

## Examples
### 01 - 2x Regions
````yaml
Mappings:
    RegionMap:
        us-east-1:
            "AMI": "ami-0947d2ba12ee1ff75"
        ca-central-1:
            "AMI": "ami-0c2f25c1f66a1ff4d"

Parameters:
  SecurityGroupDescription:
    Description: Security Group Description
    Type: String

Resources:
  EC2:
    Type: AWS::EC2::Instance
    Properties:
      # FindInMap = CloudFormation console - not aws configure get region
      ImageId: !FindInMap [RegionMap, !Ref "AWS::Region", AMI]
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

### EC2
[<img src="https://i.imgur.com/qz4d6n7.png">](https://i.imgur.com/qz4d6n7.png)

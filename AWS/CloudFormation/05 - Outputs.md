# 05 - Outputs

## Definition
* outputs at least one value - O/P after a stack was created or updated
  
## Examples
### 01 - IPv4 Public EC2
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

# Out Put
Outputs:
  WebUrl:
    Description: IPv4 Public of my EC2
    Value: !Join
      # delimiter
      - ''
      - - 'http://'
        - !GetAtt
          - EC2
          - PublicDnsName
````

### CloudFormation
* Outputs
    * DNS_EC2_Public:
    
[<img src="https://i.imgur.com/I4D2WcB.png">](https://i.imgur.com/I4D2WcB.png)

### Browser
* No WebSRV so nothing :

[<img src="https://i.imgur.com/9HdQCsd.png">](https://i.imgur.com/9HdQCsd.png)

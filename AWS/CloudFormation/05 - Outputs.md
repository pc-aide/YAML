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

---

### 02 - CreateBucket + URLOfBucket (as O/P)
* Use Case: static WebSite  on a Bucket
````yaml
Description: Template will create an S3 bucket & O/P as URL of this Bucket
Resources:
  # Bucket
  DemoCFBucket:
    Type: AWS::S3::Bucket
    Properties:
      # BuckName only lower case
      BucketName: demo-01-cf-output-urlbucket

# O/P - stack template
Outputs:
  WebsiteURL:
    Value: !GetAtt [DemoCFBucket, WebsiteURL]
    Description: URL of my Bucket
````

#### CloudFormation
* OutPuts
    * http://demo-01-cf-output-urlbucket.s3-website.ca-central-1.amazonaws.com
    
[<img src="https://i.imgur.com/H8Q7Nff.png">](https://i.imgur.com/H8Q7Nff.png)

#### Bucket
* Browser
    * nothing in there so nothing (404)

[<img src="https://i.imgur.com/MAfF5Sd.png">](https://i.imgur.com/MAfF5Sd.png)

* if a delete this stack-template, so this buck will be gone:

[<img src="https://i.imgur.com/Fu5cWWZ.png">](https://i.imgur.com/Fu5cWWZ.png)

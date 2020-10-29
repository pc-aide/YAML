# 03 - Parameter

## Doc

## Note
* By default - no order, so can put the `parameter` to the top or bottom

## Siwtchs (optional)

---

## SRC
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

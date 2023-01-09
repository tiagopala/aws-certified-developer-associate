# AWS Cloudformation

<img height=100px; alt="cloudformation_logo" src="../../../images/cloudformation.png" />

<p>&nbsp;</p>

AWS Cloudformation is a **infrastructure as a code (iaas) service** responsible for the **management and provisioning aws resources**.

Alguns benefícios de se usar o cloudformation:

- Maior segurança dos recursos que estão sendo provisionados em todos os ambientes que o template for aplicado.
- Facilidade e rapidez na configuração de novos recursos devido a padronização do template.
- Controle de versão dos templates, possibilidando rollbacks e a remoção de todos os recursos presentes na stack se necessário.
- Serviço gratuito, custos apenas nos recursos provisionados à partir dele.

## Key Words

- Resources - Serviços provisionados.
- Template - Arquivo de configuração padronizado para provisionamento dos recursos.
- Stack - Aplicação do template na aws, recursos já provisionados.

## How Cloudformation Works?

Primeiramente devemos realizar a construção de nosso arquivo cloudformation, podendo ser em ```.yaml``` ou ```.json```.

O Cloudformation irá realizar o *upload* de seu template para o S3 e irá começar a ler o arquivo para provisionar os recursos desejados.

### Cloudformation Template

Exemplo:

```yml
AWSTemplateFormatVersion: '2010-09-09'
Metadata:
  License: Apache-2.0
Description: 'Description for provisioning ec2 resources'
Parameters:
  KeyName:
    Description: Name of an existing EC2 KeyPair to enable SSH access to the instance
    Type: AWS::EC2::KeyPair::KeyName
    ConstraintDescription: must be the name of an existing EC2 KeyPair.
  InstanceType:
    Description: WebServer EC2 instance type
    Type: String
    Default: t3.small
    AllowedValues: [t2.micro]
    ConstraintDescription: must be a valid EC2 instance type.
  SSHLocation:
    Description: The IP address range that can be used to SSH to the EC2 instances
    Type: String
    MinLength: 9
    MaxLength: 18
    Default: 0.0.0.0/0
    AllowedPattern: (\d{1,3})\.(\d{1,3})\.(\d{1,3})\.(\d{1,3})/(\d{1,2})
    ConstraintDescription: must be a valid IP CIDR range of the form x.x.x.x/x.
  LatestAmiId:
    Type:  'AWS::SSM::Parameter::Value<AWS::EC2::Image::Id>'
    Default: '/aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2'
Resources:
  EC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: !Ref 'InstanceType'
      SecurityGroups: [!Ref 'InstanceSecurityGroup']
      KeyName: !Ref 'KeyName'
      ImageId: !Ref 'LatestAmiId'
  InstanceSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Enable SSH access via port 22
      SecurityGroupIngress:
      - IpProtocol: tcp
        FromPort: 22
        ToPort: 22
        CidrIp: !Ref 'SSHLocation'
Outputs:
  InstanceId:
    Description: InstanceId of the newly created EC2 instance
    Value: !Ref 'EC2Instance'
  AZ:
    Description: Availability Zone of the newly created EC2 instance
    Value: !GetAtt [EC2Instance, AvailabilityZone]
  PublicDNS:
    Description: Public DNSName of the newly created EC2 instance
    Value: !GetAtt [EC2Instance, PublicDnsName]
  PublicIP:
    Description: Public IP address of the newly created EC2 instance
    Value: !GetAtt [EC2Instance, PublicIp]
```

Algumas das seções em que se divide o cloudformation são: **Metadata**, **Description**, **Parameters**, **Mappings**, **Transform**, **Resources** e **Outputs**. Porém todas são opcionais com exceção da seção de resources que é obrigatória e destinada ao provisionamento dos serviços.

Importante lembrar que a seção Transform, pode ser usada tanto para referenciar códigos - e.g. código lambda - ou *templates snippets* - partes de templates reutilizáveis - promovendo a reutilização de código.

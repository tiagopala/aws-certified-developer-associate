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

Algumas das seções em que se divide o cloudformation são: **Metadata**, **Description**, **Parameters**, **Mappings**, **Transform**, **Resources** e **Outputs**. Porém todas são opcionais com exceção da seção de resources que é obrigatória e destinada ao provisionamento dos serviços.

Importante lembrar que a seção Transform, pode ser usada tanto para referenciar códigos - e.g. código lambda - ou *templates snippets* - partes de templates reutilizáveis - promovendo a reutilização de código.

- [Cloudformation Template Example](#cloudformation-template-example)

### Cloudformation Stack Values

Basicamente os stack values são utilizados para **importar e exportar variáveis** provenientes de **diferentes cloudformation templates**.

Imagine o seguinte cenário: O departamento de CloudSecOps possui um template responsável por provisionar uma nova VPC contendo uma *public subnet* e uma *private subnet*, um *security group*, um *network acl* e um *internet gateway*, que será utilizado pelos outros departamentos para lançar suas próprias instâncias ec2. Agora imagine um sub departamento querendo lançar algumas instâncias ec2 a qual estarão seus respectivos produtos. Para que este vínculo seja feito corretamente, o time de CloudSecOps apenas tem que exportar as variáveis referentes as *subnets* e *security groups* em seu template e assim que os times forem lançar seus produtos, em seus respectivos *cloudformation templates* devem apenas adicionar como parâmetro de entrada o nome da *stack* à qual provisionou a VPC e dar um *replace* dentro de seu cloudformation, como pode ser visto nos exemplos abaixo.

Exemplo CloudSecOps VPC Template:
```yml
Outputs:
  VPCId:
    Description: Newly created VPC
    Value: !Ref "VPC"
    Export: 
      Name: !Sub "${AWS::StackName}-VPCID"
  PublicSubnet:
    Description: Newly created subnet from VPC above
    Value: !Ref "PublicSubnet"
    Export:
      Name: !Sub "${AWS::StackName}-SubnetID"
  WebServerSecurityGroup:
    Description: Newly created security group from subnet above
    Value: !GetAtt WebServerSecurityGroup.GroupId
    Export:
      Name: !Sub "${AWS::StackName}-SecurityGroupID" 
```

Exemplo Other Departments Template:
```yml
Parameters:
  NetworkStackParameter:
    Type: String
Resources:
  WebServerInstance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t2.micro
      ImageId: ami-0ed9277fb7eb570c9
      NetworkInterfaces:
      - GroupSet:
        - Fn::ImportValue:
            Fn::Sub: "${NetworkStackParameter}-SecurityGroupID"
        AssociatePublicIpAddress: 'true'
        DeviceIndex: '0'
        DeleteOnTermination: 'true'
        SubnetId:
          Fn::ImportValue:
            Fn::Sub: "${NetworkStackParameter}-SubnetID"     
```

##### Cloudformation Template Example

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

### Cloudformation Nested Stacks

O **Cloudformation Nested Stacks** é uma feature que permite a um cloudformation template referenciar um outro template, possibilitando a não geração de duplicidade de código, faciltiando o gerenciamento de recursos compartilhados por diversas stacks e principalmente tendo o reaproveitamento de templates cloudformation.

> Como o próprio nome diz é uma feature para gerar *cloudformation template* aninhados.

Para criarmos um cloudformation que referencia à outro (nested stack template), simplesmente devemos criar um recurso com do tipo ```AWS::CloudFormation::Stack``` e referenciar o template localizado dentro de seu bucket de acordo com o exemplo abaixo:

```yml
AWSTemplateFormatVersion: '2010-09-09'
Resources:
  myStack:
    Type: AWS::CloudFormation::Stack
    Properties:
      TemplateURL: https://s3.amazonaws.com/cloudformation-templates-tiagopala/S3_Bucket.template # Único campo obrigatório
      TimeoutInMinutes: '60'
Outputs:
  StackRef:
    Value: !Ref myStack
```

## SAM (Serverless Application Model) 

O SAM é uma **Extensão do CloudFormation** para construção de **aplicações serverless** utilizando um **template específico** e seu próprio CLI, o **AWS SAM CLI**.

Os templates via SAM possuem uma configuração mais simples e possui uma fácil integração com outros recursos serverless. Sempre que estiver trabalhando com recursos serverless a utilização do SAM é fortemente indicada.

Ele pode ser baixado diretamente da documentação da aws, de acordo com o seguinte link: [Installing AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html#install-sam-cli-instructions).

SAM Template Example:

```yml
AWSTemplateFormatVersion: 2010-09-09
Description: >-
  sam-app
Transform:
- AWS::Serverless-2016-10-31

Resources:
  helloFromLambdaFunction:
    Type: AWS::Serverless::Function
    Properties:
      Handler: src/handlers/hello-from-lambda.helloFromLambdaHandler
      Runtime: nodejs12.x
      Architectures:
        - x86_64
      MemorySize: 128
      Timeout: 100
      Description: A Lambda function that returns a static string.
      Policies:
        - AWSLambdaBasicExecutionRole
```

> Uma grande feature do AWS SAM, é podermos testar nossas *lambdas* em ambiente local.

### Some SAM CLI Commands

- ```sam package``` - Criar um pacote de deployment da sua aplicação e subir para um bucket S3 informado.

- ```sam deploy``` - Realizar o deploy da sua aplicação serverless à partir um template SAM localizado no bucket s3 informado.
  > Por baixo dos panos o SAM irá realizar o deploy via Cloudformation.
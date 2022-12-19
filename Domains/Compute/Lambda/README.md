# AWS Lambda

<img height=100px; alt="ec2_logo" src="../../../images/lambda.png" />

<p>&nbsp;</p>

AWS Lambda is a **serverless compute service**, responsible for **running code without managing any servers**.

> AWS Lambda é um dos serviços mais importantes da aws, podendo até ser considerado o mais importante de todos.

## How it works?

A lambda utiliza uma arquitetura de eventos (***event-driven architecture***) para execução de seus jobs. Podendo ser automaticamente *'triggados'* por outros serviços da aws, ou chamados diretamente por *web apps* ou *mobile apps*.

> A integração entre o API Gateway + Lambda é uma das mais interessantes, transformando suas lambdas em pequenas API's. Abaixo, uma lista com outros serviços que podem *'triggar'* uma *lambda function*.

## Lambda Concurrent Executions Limit

Apesar das lambdas serem um recurso serverless em que a escalabilidade é gerenciada pela própria Amazon, é importante ter em mente que existe um ***soft limit*** (limite que pode ser alterado) de **1000 execuções simultâneas** (no mesmo segundo) **por conta**.

Caso o número de execuções simultâneas seja **atingido**, próximas invocações retornarão um **HTTP Status Code 429 - Too Many Requests**. Para resolvermos este problema, devemos apenas abrir uma **solicitação para aumentar o limite**.

> Importante lembrar que podemos configurar o **reserved concurrency**, que são um número de execuções que estão **sempre disponíveis** para **funções críticas**.

## Lambda Versioning

A lambda possui suporte para **versionamento** de código de uma maneira muito simples. Por **padrão** a lambda sempre utiliza a versão **$LATEST** que corresponde a **versão mais atualizada**. Quando utilizamos o ARN de uma lambda, por padrão sempre referenciamos o $LATEST ao menos que seja informado a **versão** ou ***alias*** desejado.

Como comentado acima, para **cada versão** de nosso código podemos ter **diferentes alias** que são basicamente formas de nomear uma versão com alguma finalidade específica. Por exemplo, vamos imaginar que a versão 1 da nossa lambda corresponde ao código que está em produção e portanto não desejamos alterá-la para testes, assim iremos criar um alias para a versão 1, subir uma nova versão (versão 2) e criar um *alias* para a versão 2 que corresponderá ao nosso ambiente de testes, assim conseguiremos dividir os escopos sem um impactar ao outro.

Abaixo a visualização do exemplo acima: 

**Produção** (versão/alias):
- arn:aws:lambda:sa-east-1:123456789012:function:mylambda:**1** -> arn:aws:lambda:sa-east-1:123456789012:function:mylambda:**Prod**

**Testes** (versão/alias):
- arn:aws:lambda:sa-east-1:123456789012:function:mylambda:**2** -> arn:aws:lambda:sa-east-1:123456789012:function:mylambda:**Test**

**Código atual**
- arn:aws:lambda:sa-east-1:123456789012:function:mylambda:**$LATEST**

> Importante lembrar que caso realizemos a atualização do código ($LATEST), porém os serviços integrados estão utilizando o alias de prod, não será atualizado automaticamente com a versão mais recente de nosso código. 

## Accessing Resources inside Private VPC

É possível que nossa lambda se comunique com recursos dentro de uma VPC, porém é necessário algumas configurações para que isto ocorra.

Esta configuração pode ser realizada via **AWS CLI** ou pelo próprio **console**. Primeiramente precisamos informar os seguintes dados - **private subnet id** e **security group id** - da VPC em que os recursos estão localizados.

A lambda utilizará os seguintes dados para configurar um **Elastic Network Interface (ENI)** utilizando um IP disponível dentro do CIDR range da subnet e assim será possível acessar os recursos desejados dentro da VPC.

## Lambda Triggers

- Api Gateway
- ALB
- Alexa
- S3
- DynamoDb
- Kinesis
- SQS
- SNS
- SES
- Cloudfront
- Cloudformation
- CloudWatch
- CodeCommit
- CodePipeline

## Supported Languages

- C#
- Java
- Go
- NodeJs
- Python
- Ruby
- Powershell

## Pricing

- Requests
- Duration
- Price per GB-second

> O *Free Tier* da lambda é extremamente generoso, sendo um dos serviços mais baratos da aws (**extremely cost effective**).
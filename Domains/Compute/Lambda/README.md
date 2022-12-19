# AWS Lambda

<img height=100px; alt="ec2_logo" src="../../../images/lambda.png" />

<p>&nbsp;</p>

AWS Lambda is a **serverless compute service**, responsible for **running code without managing any servers**.

> AWS Lambda é um dos serviços mais importantes da aws, podendo até ser considerado o mais importante de todos.

## How it works?

A lambda utiliza uma arquitetura de eventos (***event-driven architecture***) para execução de seus jobs. Podendo ser automaticamente *'triggados'* por outros serviços da aws, ou chamados diretamente por *web apps* ou *mobile apps*.

> A integração entre o API Gateway + Lambda é uma das mais interessantes, transformando suas lambdas em pequenas API's. Abaixo, uma lista com outros serviços que podem *'triggar'* uma *lambda function*.

### Lambda Triggers

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

#### Supported Languages

- C#
- Java
- Go
- NodeJs
- Python
- Ruby
- Powershell

## Versioning

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

## Pricing

- Requests
- Duration
- Price per GB-second

> O *Free Tier* da lambda é extremamente generoso, sendo um dos serviços mais baratos da aws (**extremely cost effective**).
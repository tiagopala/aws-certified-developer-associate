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

## Pricing

- Requests
- Duration
- Price per GB-second

> O *Free Tier* da lambda é extremamente generoso, sendo um dos serviços mais baratos da aws (**extremely cost effective**).
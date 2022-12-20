# AWS X-RAY

<img height=100px; alt="x-ray_logo" src="../../../images/x-ray.png" />

<p>&nbsp;</p>

AWS X-Ray is a **developer tool service** which provides features for **analysis and debugging distributed applications**.

O X-Ray fornece um ***service map*** que é basicamente uma **representação visual** da nossa aplicação e todas suas integrações. Através dele podemos ver a **latência**, os **status codes** e possíveis **erros**.

Requisições feitas da sua aplicação para outros serviços da aws também são capturados de forma automática pela sdk do x-ray.

## How it works?

Para utilizarmos o x-ray em nossas aplicações é necessário seguir os seguintes passos:

1. Instalar o agente do x-ray em nossa instância EC2.
2. Instrumentar a aplicação usando o sdk do x-ray.

Após esta configuração o x-ray automaticamente já irá capturar *requests* e *responses* e enviar o *tracing* para o x-ray.

## Integrations

- EC2
- ECS
- Lambda
- Elastic Beanstalk
- SNS
- DynamoDb
- ELB
- API Gateway

> Podemos utilizar o x-ray com as seguintes linguagens: .NET, Java, NodeJS, Go, Ruby e Python.
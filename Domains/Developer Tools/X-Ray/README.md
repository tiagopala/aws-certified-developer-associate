# AWS X-RAY

<img height=100px; alt="x-ray_logo" src="../../../images/x-ray.png" />

<p>&nbsp;</p>

AWS X-Ray is a **developer tool service** which provides features for **analysis and debugging distributed applications**.

O X-Ray fornece um ***service map*** que é basicamente uma **representação visual** da nossa aplicação e todas suas integrações. Através dele podemos ver a **latência**, os **status codes** e possíveis **erros**.

Requisições feitas da sua aplicação para outros serviços da aws também são capturados de forma automática pela sdk do x-ray.

## How it works?

Para utilizarmos o x-ray em nossas aplicações é necessário seguir os seguintes passos:

1. Instalar o agente do **x-ray daemon** em nossa instância EC2 ou *on-premises server*.
2. Instrumentar a aplicação usando o **x-ray sdk**.

> Para o Elastic Beanstalk devemos instalar o x-ray daemon em nosso *Elastic Beanstalk Environment*. No caso do ECS, devemos instalá-lo em um docker container próprio para X-Ray dentro do *cluster* ECS junto à sua aplicação. Caso seja instalado junto ao container da própria aplicação não irá funcionar.

Após esta configuração o x-ray automaticamente já irá capturar *requests* e *responses* e enviar o *tracing* para o x-ray.

## Annotations & Indexing

Além de capturar os metadados de cada requisição, é possível incluir **annotations** que são basicamente **dados adicionais** enviados juntamente aos metadados para o x-ray que serão **indexados** à fim de serem utilizados em ***filter expressions***.

O formato em que os dados são salvos é através de ***key-value pairs*** de acordo com o exemplo abaixo.

> Exemplo: onboarding_id:513348B8-7A20-442D-8507-E4D809F1F3F2

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
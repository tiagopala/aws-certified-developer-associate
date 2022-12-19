# Amazon API Gateway

<img height=100px; alt="api-gateway_logo" src="../../../images/api-gateway.png" />

<p>&nbsp;</p>

Amazon API Gateway is aws' own API service.

Através dele podemos **publicar**, **gerir** e **monitorar API's** em qualquer escala.

Permite a criação de endpoints únicos para cada interação necessária.

> É um serviço ***serverless***!

## API Concepts

API significa ***Application Programming Interface*** e seu papel é de fazer uma ponta entre aplicações, sejam elas frontend ou backend, permitindo a todos esses serviços se comunicarem de uma forma padronizada.

> O formato utilizado para a comunicação é o **JSON** (*Javascript Object Notation*).

## Types

- **RESTful APIs** - São otimizados *stateless* (não armazenam estado) e *serverless workloads* ("processos").
- **Websocket APIS** - São utilizados serviços de tempo real, de dois sentidos e *stateful workloads*, exemplo: chats.

## Features

- **Versioning** - Suporte para múltiplas versões ao mesmo tempo.
- **Logging using Cloudwatch** - Logging de chamadas, latências e taxas de erros através do cloudwatch.
- **Throttling** - Suporte a throttling para facilitar o gerenciamento da quantidade de chamadas para os serviços backend.
    > Throttling significa interromper chamadas que superem uma quantidade de requisições por segundo para não impactar nos serviços backend, finalizando a requisição logo na ponta.


## AWS Services Integration

Atualmente o API Gateway pode integrar-se com diversos serviços como, ec2, lambda, elastic beanstalk, dynamodb e kinesis.
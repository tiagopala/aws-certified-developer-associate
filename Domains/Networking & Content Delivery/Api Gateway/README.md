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
- **Logging using Cloudwatch** - *Logging* de chamadas, latências e taxas de erros através do cloudwatch.
- **Import existing APIs** - O API Gateway possui suporte para importação de API's utilizando o formato OpenAPI.
- **Legacy Protocols Support** - O API Gateway possui suporte para trabalhar com protocolos legados como **SOAP** através das seguintes formas: Configurando o API Gateway como um **SOAP web service** ou podemos utilizar o API Gateway apenas para **converter responses XML em JSON**.
- **Caching** - Armazena o *response* de uma requisição em *memory cache* por um *TTL* (default 300s) e assim que uma nova requisição igual for solicitada, ele irá retornar o *response* já *'cacheado'*. É uma *feature* que promove aumento de performance. 
- **Throttling** - Suporte a throttling para facilitar o gerenciamento da quantidade de chamadas para os serviços backend.
    > Throttling significa interromper chamadas que superem uma quantidade de requisições por segundo para não impactar nos serviços backend, finalizando a requisição logo na ponta.Valores limites por padrão: 10.000 RPS (*requests per second*) e 5.000 requisições concorrentes. Caso esses valores sejam atingidos, futuras requisições irão receber um status code 429 (*too many requests*). Esses valores são apenas *soft limits* e podem ser alterados.

## AWS Services Integration

Atualmente o API Gateway pode integrar-se com diversos serviços como, ec2, lambda, elastic beanstalk, dynamodb e kinesis.

## Tips

- O Api Gateway possui stage variables fazendo com que ele possa interagir com diferentes backends.

- O Api Gateway Mapping Templates pode ser usado para mapear outros formatos de requests/responses.

- O Api Gateway Usage Plans permite controlar quem pode acessar a nossa API.

- O Api Gateway não possui suporte para o STS.

- O Api Gateway possui os tipos: Rest Api, HTTP Api e Web Socket.

- Através de uma HTTP Api, não é possível integrar-se com o AWS Web Application FireWall (WAF), apenas através de uma Rest Api.
    > As HTTP Api são mais simples e portanto não possuem grande parte das features que da Rest Api.

- Devemos utilizar lambda authorizers quando o objetivo for  realizar uma autenticação customizada utilizando um token JWT, como o OAuth ou SAML.

- Api gateway possui suporte nativo para criação de Mocks.

- Se nosso Api Gateway possuir caching, podemos invalidá-lo através de uma requisição HTTP incluindo o header ```Cache-Control``` com o valor ```max-age=0```. Lembrando que para conseguirmos passar este parâmetro, devemos possuir as devidas permissões.
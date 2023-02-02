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

## Tips

- Não é possível configurar o CPU de uma lambda, devemos aumentar a memória e a própria lambda irá aumentar proporcionalmente a quantidade de CPU. Inclusive, essa é uma forma de aumentarmos a performance de uma lambda, é justamente aumentando a memória, consequentemente o tempo de execução desta lambda também irá diminuir.

- Uma boa prática para melhorar a performance das lambdas é extrair arquivos de inicializam e client database connections para fora do handler, para dentro da execution context para ser reaproveitado por outras execuções.

- Sempre devemos optar primeiro pelas boas práticas, como a remoção de arquivos de inicializam comentados acima e só depois optarmos pelo aumento do poder computacional das lambdas.

- Separar o handler do core business logic (regra de negócio) facilita tanto o reúso de código quanto a implementação de testes unitários.

- Para uma lambda conseguir estabelecer conexão com uma subnet privada dentro de uma VPC, ela deve possuir em sua executation role as seguintes policies ec2:CreateNetworkInterface, ec2:DescribeNetworkInterface e ec2:DeleteNetworkInterface, além de habilitar acesso para a lambda no security group associado.

- Sempre que uma lambda é "invokada" através de um unqualified ARN, é chaamdo o $LATEST que corresponde a versão mais atualizada desta lambda, a menos que seja passado o ALIAS ou VERSION.

- A lambda possui diversos triggers, podendo eles serem síncronos ou assíncronos, alguns deles:
    - Síncronos: Api Gateway, ALB
    - Assíncronos: SNS Subscription

- Lambda possuem environment variables, não possuem limite de quantidade de variáveis, porém todas as variáveis somadas não podem ter tamanho superior a 4 Kb.

- Podemos criar lambdas como containers, para isso devemos criar a lambda function na mesma conta do ECR em que a imagem dela foi armazenada e que esta imagem possua uma implementação para a Lamda Runtime API.

- Apesar da lambda ser um recurso serverless, podemos colocar um Auto Scaling na frente dela para gerenciarmos o uso da provisioned concurrency em um intervalo de tempo determinado.

- O seguinte erro: "Error: Memory Size: XXX Mb Max Memory Used" significa que atingimos o limite de memória daquela lambda e devemos provisionar mais memória para futuras execuções.

- Caso nossa lambda necessita de alguma dependência (library externa) devemos fazer o download destas dependências dentro da própria lambda em um folder específico, "zipar" a lambda junto as dependências e realizar o deploy.

- Para fazer o deploy de lambdas globalmente devemos usar o Lambda@Edge.

- Para fazer o deploy de uma lambda através do cloudformation:
    1. Zip da lambda, subir no s3, referenciar o arquivo s3 no template e realizar o deploy do template na aws.
    2. Escrever o próprio código da lambda inline no template e realizar o deploy do template na aws.

- Para armazenarmos arquivos localmente durante a execução de uma lambda que serão removidos após seu processamento devemos usar o local directory /tmp.

- Referente ao modelo de concorrência das lambdas, a quantidade máxima de lambdas que podem ser invocadas simultaneamente por conta AWS possui um soft limit. Porém, em cenários que uma lambda seja crítica e precisamos garantir que tenha poder computacional disponível para ela escalar sem causar *throttling*, podemos usar a *reserved concurrency*. Dessa forma, essas lambdas ficam "reservadas" apenas para esta lambda caso seja necessário.

- Outro recurso que é importante termos em mente sobre lambdas é o *provisioned concurrency*, ele nos permite aumentar a performance de nossas lambdas através do *warm up* prévio das lambdas.
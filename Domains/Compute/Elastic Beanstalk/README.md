# AWS Elastic Beanstalk

<img height=100px; alt="elastic-beanstalk-logo" src="../../../images/elastic-beanstalk.png" />

<p>&nbsp;</p>

AWS Elastic Beanstalk is a **compute service** that helps to **deploy and scale web applications**.

O Elastic Beanstalk é o serviço mais **fácil e rápido** de se realizar **deploys e escalar aplicações web**. Através dele podemos apenas nos concentrar em nosso código pois ele fica responsável por prover os recursos necessários, realizar o update da aplicação e sistema operacional, além de possuir monitoramento, métricas e health checks inclusos.

O controle dos recursos pode ficar apenas como responsabilidade do Beanstalk, porém é possível "assumir o controle" e gerenciar os recursos por conta própria, alterando suas configurações, como também alterar a arquitetura provisiondada por ele.

> Para realizar o deploy de novas versões basta subirmos a nova versão para o elastic beanstalk, selecionarmos o environment (ambiente) e pronto, o elastic beanstalk se encarregará de fazer o deploy de acordo com as configurações presentes na seção **rolling updates and deployments**.

## How to Customize EB Environment?

Podemos customizar nossos ambientes através de diferentes maneiras. A primeira diferença que temos é devido ao tipo de sistema operacional que estamos utilizando, divididos em Amazon Linux 1 e 2.

Em instâncias do tipo **Amazon Linux 1**, devemos criar um folder chamado ```.ebextensions``` na raíz (top-level directory) do bundle da aplicação e os arquivos devem possuir a extensão ```.config```, como por exemplo: ```myautoscaling.config```.

Em instâncias do tipo **Amazon Linux 2**, podemos criar um arquivo chamado ```Buildfile``` no diretório raíz da nossa aplicação para comandos que são finalizados após execução (exemplo: shell scripts). Podemos criar um arquivo chamado ```Procfile``` para processos de longa duração (*long-running processes*) e também podemos criar **Platform Hooks** de acordo com o seguinte exemplo: ```.platform/hooks/ENVIRONMENT_NAME```, para execução de scripts e executáveis em diferentes estágios do provisionamento das instâncias EC2. 

> Os environments podem ser: ```prebuild```, ```predeploy``` e ```postdeploy```.
>
> Exemplo: ```.platform/hooks/prebuild```

## RDS Inside x Outside Beanstalk Environment

Basicamente temos duas formas de integrarmos nosso *environment* do Beanstalk com uma base de dados RDS, porém devemos nos atentar aos detalhes de cada uma.

### RDS Inside Beanstalk

Neste primeiro cenário nosso RDS fica junto aos outros recursos dentro do próprio *environment* do Beanstalk. Porém esta opção não deve ser utilizada em um ambiente produtivo, pois caso seja necessário realizar o *shut down* do *environment*, perderemos todo os dados presentes em nossa base de dados, pois ela será excluida juntamente ao nosso *environment*. Deve ser uma opção apenas para os ambientes de *dev* e *testing*.

### RDS Outside Beanstalk

Neste segundo cenário, nossa base de dados RDS fica apartada, assim caso seja necessário realizar o shut down do *environment*, não teremos impactos em nossa base de dados. Este cenário é aconselhável para um ambiente produtivo.

Porém, para estabelecermos essa integração devemos:

1. Criar um *security group* adicional.
2. Informar a *connection string* e *database password* nas *environment properties* do *beanstalk environment*.

## Deployment Types

### All At Once Deployment

Realiza o deploy em todas as instâncias de uma só vez. Implica interrupção total do serviço durante o deploy, o mesmo ocorre em cenário de rollback.

![elastic-beanstalk-all-at-once-deployment](../../../images/elastic-beanstalk-all-at-once-deployment.drawio.png)

### Rolling Deployment (Batches)

Capacidade reduzida durante o deploy, pois uma parte (batch) ficará indisponível enquanto o deploy é realizado, tendo perda parcial na capacidade, o mesmo cenário ocorre para o rollback.

![elastic-beanstalk-rolling-deployment](../../../images/elastic-beanstalk-rolling-deployment.drawio.png)

### Rolling Deployment Additional Batch

Mantém a capacidade total durante o deploy.

![elastic-beanstalk-rolling-deployment-additional-batch](../../../images/elastic-beanstalk-rolling-deployment-additional-batch.drawio.png)

### Immutable Deployment

O deploy consiste em subir primeiro as novas instâncias que possuem a nova versão, após passar pelos health checks, irá matar as antigas instâncias e permanecer com as novas. Não possui downtime, 0 impacto de capacidade ou interrupção para aplicação durante o deploy.

![elastic-beanstalk-immutable-deployment](../../../images/elastic-beanstalk-immutable-deployment.drawio.png)

### Traffic Splitting

Deploy ocorre da mesma forma do immutable porém somente parte das requisições são direcionadas para esta nova versão, permite ***Canary Testing***.

## Migrating existing .NET applications

A AWS aconselha o uso de uma ferramenta chamada **Windows Web Application Migration Assistant** para migração de aplicações .NET que estão atualmente rodando em *windows servers* em seu próprio data center para o *elastic beanstalk*.

É uma ferramenta *open source*, que utiliza *PowerShell* por debaixo dos panos para realizar a migração da aplicação, ela também é usualmente chamada de **.NET Migration Assistant** pela comunidade.

## Programming Languages

As linguagens permitidas atualmente são: .NET, Java, PHP, Python, Ruby, Go e NodeJs.

## Managed Platforms

Podemos realizar o *deploy* da nossa aplicação em um servidor Apache Tomcat ou realizar o deploy através de uma imagem/container via Docker.

### Deploying using Docker Containers

Através do *deploy* via docker containers, temos duas opções: **single docker container** ou **multi-container docker**.

Para a opção *single docker container*, o Elastic Beanstalk irá provisionar uma única instância ec2 para rodar seu docker container.

Já se escolhermos o deploy de múltiplos containers (*multi-container docker*) o Elastic Beanstalk irá criar um **cluster ecs** para rodar os múltiplos containers. 

> Através da página de versões da aplicação (application versions page) podemos voltar para uma versão anterior (previous version) realizando o deploy desta versão novamente em nosso ambiente.

## AWS Resources

Alguns dos recursos que o Beanstalk pode promover são: EC2, RDS, S3, Elastic Load Balancer, Auto Scaling Groups, entre outros.

## Tips

- O código fonte '*deployado*' através do elastic beanstalk também pode ser armazenado no CodeCommit, além de ser realizado manualmente via uploado do zip no próprio console da aws.

- As plataformas suportadas pelo Elastic Beanstalk são: .NET, Java, PHP, Python, Ruby, Go, Nodejs, Docker e Tomcat.

- Sobre o modelo de configuração do Elastic Beanstalk:
    1. Para instâncias do tipo Amazon Linux 1, devemos obrigatoriamente ter um folder chamado .ebextensions e arquivos de configuração com a extensão .config dentro.
    2. Para instâncias do tipo Amazon Linux 2, o folder .ebextensions é opcional e devemos usar o BuildFile, ProcFile e Platform Hooks.

- As cores utilizadas para indicar os status do deployment no Elastic Beanstalk são:
    1. Gray: Updating
    2. Yellow: Failed 1 or more health checks.
    3. Red: Failed 3 or more health checks.
    4. Green: Passed all health checks.

- O Elastic Beanstalk não possui suporte para lambdas.

- O Elastic Beanstalk Rolling Deployment possui capacidade reduzida porém não possui downtime durante deployment.

- Se quisermos fazer o deploy de uma plataforma não suportada pelo Elastic Beanstalk podemos criar nossa própria plataforma utilizando-se do Packer.

- Por baixo dos panos o Elastic Beanstalk utiliza o Cloudformation para provisionamento dos recursos.

- Se quisermos provisionar um recurso junto ao nosso environment, devemos defini-lo dentro do nosso .ebextensions folder.

- Os tipos de deployment Immutable e Traffic Splitting utilizam o burst balance acumulados.

- Entre os tipos de deployment disponíveis, se quisermos maior rapidez em um cenário de falha que envolva rollback devemos optar pelo Immutable deployment.

- Elastic Beanstalk consegue fazer deploy o deploy de containers no ECS utilizando instâncias EC2, se quisermos utilizar instâncias Fargate, devemos utilizar o EC2 + Fargate diretamente.

- Para aplicações que executam um processo de longa duração, devemos utilizar Dedicated Worker environments.
    > Eles também pode ser usadas para consumir mensagens provenientes do SQS.

- Se quisermos possuir duas versões de uma aplicação rodando ao mesmo tempo utilizando o Elastic Beanstalk devemos criar um environment para cada uma delas.

- Se tivermos um ALB provisionado dentro de nosso environment, que está sendo usado para armazenar a sessão do usuário, para cada novo deployment da aplicação iremos perder o conteúdo armazenado no ALB. Para isso é aconselhável que tenhamos um recurso definido externamente do nosso environment, como por exemplo um elasticache.

- O Elastic Beanstalk possui suporte nativo a lifecycle policies. Através delas podemos, por exemplo, criar policies que deletem versões anteriores que não estão mais sendo utilizadas.

- Se precisarmos definir tarefas repetitivas e "scheduladas" (agendadas), devemos criar um Worker Environment junto a um arquivo cron.yml.
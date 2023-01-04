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

## Deployment Types

### All At Once Deployment

Realiza o deploy em todas as instâncias de uma só vez. Implica interrupção total do serviço durante o deploy, o mesmo ocorre em cenário de rollback.

![elastic-beanstalk-all-at-once-deployment](../../../images/elastic-beanstalk-all-at-once-deployment.drawio.png)

### Rolling Deployment (Batches)

Capacidade reduzida durante o deploy, pois uma parte (batch) ficará indisponível enquanto o deploy é realizado, tendo perda partical na capacidade, o mesmo cenário ocorre para o rollback.

![elastic-beanstalk-rolling-deployment](../../../images/elastic-beanstalk-rolling-deployment.drawio.png)

### Rolling Deployment Additional Batch

Mantém a capacidade total durante o deploy.

![elastic-beanstalk-rolling-deployment-additional-batch](../../../images/elastic-beanstalk-rolling-deployment-additional-batch.drawio.png)

### Immutable Deployment

O deploy consiste em subir primeiro as novas instâncias que possuem a nova versão, após passar pelos health checks, irá matar as antigas instâncias e permanecer com as novas. Não possui downtime, 0 impacto de capacidade ou interrupção para aplicação durante o deploy.

![elastic-beanstalk-immutable-deployment](../../../images/elastic-beanstalk-immutable-deployment.drawio.png)

### Traffic Splitting

Deploy ocorre da mesma forma do immutable porém somente parte das requisições são direcionadas para esta nova versão, permite ***Canary Testing***.

## Programming Languages

As linguagens permitidas atualmente são: .NET, Java, PHP, Python, Ruby, Go e NodeJs.

## Managed Platforms

Podemos realizar o deploy da nossa aplicação em um servidor Apache Tomcat ou realizar o deploy através de uma imagem/container via Docker.

## AWS Resources

Alguns dos recursos que o Beanstalk pode promover são: EC2, RDS, S3, Elastic Load Balancer, Auto Scaling Groups, entre outros.
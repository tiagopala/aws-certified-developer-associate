# Amazon CloudWatch

<img height=100px; alt="cloudwatch_logo" src="../../../images/cloudwatch.png" />

<p>&nbsp;</p>

Amazon CloudWatch is a **management and governance service** responsible for **monitoring**, **logging** e **setting up alarms** for your applications.

Como mencionado acima, através do CloudWatch é possível monitorar a **saúde** e a **performance** de nossas aplicações, assim como dos recursos AWS utilizados por elas.

A gama de serviços que o CloudWatch atualmente suporta é incrivelmente extensa, integrado por quase todos os principais serviços da aws.

## Features

- [CloudWatch Monitoring](#cloudwatch-monitoring-metrics)
- [CloudWatch Logs](#cloudwatch-logs)
- [CloudWatch Alarms](#cloudwatch-alarms)

### CloudWatch Monitoring (Metrics)

Através do CloudWatch Monitoring podemos gerenciar algumas métricas que já vem por default do EC2, como também podemos criar nossas próprias métricas.

As **métricas default** no EC2 são: **CPU**, **Network**, **Disk** e **Status Check**.

#### CloudWatch Agent

Através do CloudWatch Agent podemos **criar nossas próprias métricas** e *plotarmos* no *CloudWatch* estes dados. Através dele também podemos habilitar as **Operating System-Level Metrics**, pois não são habilitadas por default, somente através do *cloudWatch agent*.

##### Operating System-Level Metrics

Algumas das métricas que compõem as *Operating System-Level Metrics* são:

- **Memory Use**.
- **Processes running in the instance**.
- **Free space disk**.
- **CPU Idle time**.

> As métricas são armazenadas por tempo indefinido e podem ser recuperadas mesmo após as instâncias do EC2 terem sido terminadas.

#### Frequency

A **frequência padrão** em que as **métricas padrão** são enviadas ao CloudWatch é de **5 minutos**. Porém podemos ligar o **monitoramento detalhado** para enviar a cada **1 minuto**.

Já as **métricas customizadas** são enviadas por padrão a cada **1 minuto**, porém pode também ser aumentada através do ***High Resolution Metrics*** e enviar a cada **1 segundo**.

Características      | Métricas Default | Métricas customizadas | 
-------------------- | ---------------- | --------------------- |
Frequência Padrão    | 5 minutos        | 1 minuto              |
Frequência Aumentada | 1 minuto         | 1 segundo             |

### CloudWatch Logs

O CloudWatch Logs como o próprio nome diz armazena os logs quase em tempo real das aplicações quanto também de recursos aws para monitoramento da saúde da aplicação quanto também auxiliar no troubleshooting em casos de erros.

É possível também capturarmos a quantidade de erros ocorrendo na aplicação para enviar notificações quando o número ultrapasse um valor previamente estabelecido.

### CloudWatch Alarms

O CloudWatch Alarms é bem sugestivo, através do monitoramento das peças e serviços, é possível '*triggar*' alarmes para praticamente qualquer cenário que esteja ocorrendo em sua conta. Podemos criar desde alarmes de cobrança sempre que a conta atinge um limite previamente estabelecido até executarmos uma policy de escalabilidade para adicionar um novo POD no Auto Scaling Group toda vez que uma instância chega aos 80% de uso de CPU, como diversos outros cenários.

Basicamente, através dele temos muita flexibilidade para criarmos alarmes ou executar tarefas baseadas no monitoramento de seus recursos e aplicações assim que atingem thresholds específicos.

## Some CloudWatch Concepts to Remember

### CloudWatch Metrics

As métricas são basicamente variáveis para monitorarmos.

Exemplo: *CPU usage of EC2 instance*.

### CloudWatch Namespaces

Os *namespaces* são basicamente container de agrupamento de métricas no console.

Podemos criar nossos próprios *namespaces*, para agrupar aplicações que possuem uma correlação.

Exemplo: Todas as métricas referentes ao *EC2* estão no namespace *AWS/EC2*.

### CloudWatch Dimensions

As *dimensions* são simplesmente filtros para buscarmos métricas específicas.

Exemplo: Para o *InstaceId*, iremos capturar todas as métricas que se referem somente a esta instância.

### CloudWatch Dashboards

São painéis que agrupam importantes métricas para suas aplicações produtivas vinculados a uma operação.

Exemplo: Agrupamento das métricas de CPU e Memoria de suas aplicações.
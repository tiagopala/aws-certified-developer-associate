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
- [CloudWatch Actions](#)

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

#### CloudWatch Actions

As CloudWatch Actions ações que podem ser utilizadas para publicar, monitorar e alertar caso com base em diversas métricas.

Devido a lista de actions extensa, segue [link para consulta](https://docs.aws.amazon.com/AmazonCloudWatch/latest/APIReference/API_Operations.html).

Podemos pensar nas actions como operações ou endpoints disponíveis pelo CloudWatch.

Por exemplo, a operação ```PutMetricData``` realiza o envio de dados para uma métrica, conforme exemplo abaixo.

```
aws cloudwatch put-metric-data \
--metric-name ErrorCounter \
--namespace ServiceName \
--value 1 \
--timestamp 2023-01-01T00:00:000Z
```

Já a operação ```PutMetricAlarm``` é responsável por criar alarms baseado em alguma métrica, podendo ser inclusive a métrica customizada acima, como podemos ver no exemplo:

```
aws cloudwatch put-metric-alarm \
--alarm-name ErrorCounterReached  \
--alarm-description "ErrorCounter Monitor" \
--metric-name ErrorCounter \
--namespace ServiceName \
--statistic SampleCount \
--period 300 \
--threshold 1 \
--comparison-operator GreaterThanThreshold \
--evaluation-periods 1
```

> Cada action possui uma responsabilidade específica, como seus parâmetros obrigatórios e podem ser consultadas no link mencionado anteriormente.

## Some CloudWatch Concepts to Remember

### CloudWatch Metrics

As métricas são basicamente variáveis para monitorarmos.

Exemplo: *CPU usage of EC2 instance*.

### CloudWatch Namespaces

Os *namespaces* são basicamente containers de agrupamento de métricas no console.

Podemos criar nossos próprios *namespaces*, para agrupar aplicações que possuem uma correlação.

Exemplo: Todas as métricas referentes ao *EC2* estão no namespace *AWS/EC2*.

### CloudWatch Dimensions

As *dimensions* são simplesmente filtros para buscarmos métricas específicas.

Exemplo: Para o *InstaceId*, iremos capturar todas as métricas que se referem somente a esta instância.

### CloudWatch Dashboards

São painéis que agrupam importantes métricas para suas aplicações produtivas vinculados a uma operação.

Exemplo: Agrupamento das métricas de CPU e Memoria de suas aplicações.

## Tips

- Os possíveis status do CloudWatch são: OK, ALARM e INSUFFICIENT_DATA

- Se quisermos enviar os logs para o s3, podemos habilitar a "CloudWatch Integration Feature for S3".

- Se quisermos capturar métricas customizadas como a memória RAM de instâncias, devemos criar CloudWatch Custom Metrics.

- Os CloudWatch Logs são automaticamente criptografados por default, e opcionalmente podemos optar por adicionar nossa própria chave de criptografia através do KMS.
    > Pode ser realizado através do seguinte comando: ```aws logs associate-kms-key```.
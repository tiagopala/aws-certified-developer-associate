# Amazon RDS - Relational Database Service

<img height=100px; alt="iam_logo" src="../../../images/rds.png" />

<p>&nbsp;</p>

Amazon RDS is a relational database service at AWS. Using RDS is possible to setup, operate and scale relational databases in the cloud.

## Engines

Atualmente as engines suportadas pelo RDS são:

- Amazon Aurora w/ PostgreSql
- Amazon Aurora w/ MySQL
- PostgreSql
- MySQL
- SQL Server
- MariaDB
- Oracle

> Amazon Aurora é a única engine *serverless*

## OLTP (Online Transaction Processing)

RDS é uma ótima opção quandos estamos tratando com o processamento de diversas pequenas transações como, por exemplo, capturar o status de um pedido, uma transação bancária, um pagamento ou até o agendamento de uma viagem. O RDS não deve ser utilizado para OLAP, neste caso, usar uma solução de *data warehousing* com o Amazon RedShift.

## Features

- [**Multi-AZ**](./README.md#multi-az) - disaster recovery (DI) & automatic failover capabilities
- [**Read Replicas**](./README.md#read-replicas) - performance

### Multi-AZ

Basicamente, o Multi-AZ é uma feature para **disaster recovery**.

Todas as operações que ocorrerem em nossa base de dados **primária** serão **replicados automaticamente** para uma instância **secundária**, assim temos sempre as duas bases *'syncadas'*.

![rds-multi-az](../../../images/rds-multi-az.drawio.png)

Caso ocorra algum **problema** em nossa instância **primária** ou por algum motivo perdermos a conexão com a nossa instância primária, a **própria aws** se encarrega de automaticamente redirecionar (***automatic failover***) o fluxo para a instância **secundária** enquanto a primária não retorna, como podemos ver na imagem abaixo.

![rds-multi-az-failure](../../../images/rds-multi-az-failure.drawio.png)

### Read Replicas

Já as Read Replicas devem ser usadas para um ganho de performance. Elas são basicamente cópias da nossa base de dados primária, porém, somente leitura.

Cada read replica possuirá seu próprio endpoint em que podemos nos conectar diretamente, sendo um de seus papeis de *desafogar* nossa base de dados primária.

> Uma premissa para conseguirmos habilitar as read replicas é estar com o **automated backup ligado**.

Importante lembrar também que as read replicas podem ser na **same AZ**, **cross-AZ** e **cross-region**.

![rds-multi-az-failure](../../../images/rds-read-replica.drawio.png)

## Backups

- **Automated Backups**
- **Snapshots**

#### Automated Backup

Os automated backups já são habilitados por default.

- **Point-In-Time Recovery** - Permite retornarmos nossa base para qualquer estado dentro de 1 à 35 dias.
- **Full Daily Backup** - Realiza um backup diário ou criação de um snap e armazena os *transaction logs*.

O processo de backup (***backup process***) ocorrerá em uma janela de tempo previamente configurada, em que o I/O será suspenso por alguns segundos e durante o processo de inicialização do backup podemos ter aumento na latência.

O processo de recuperação (***recovery process***) iniciará a partir do backup diário mais recente de acordo com a hora de recuperação informada pelo usuário e junto aos transaction logs, retornará o estado exatamente como estava no segundo solicitado.

To Remember

- Os backups são armazenados no S3.
- O espaço gratuito é equivalente ao tamanho da base de dados.

#### Snapshots

- Os snapshots devem ser ***"startados"*** manualmente, não são automáticos.
- Não possuem período de retenção, inclusive, se eventualmente deletarmos a própria base de dados e backups, o snapshot ainda permanecerá.
- O processo de recuperação através de um snapshot retornará a nossa base de dados para o período exato no tempo em que aquele snapshot foi tirado.

### Restoring

Caso seja necessário realizar o restore da nossa base de dados, seja ele atráves de um automated backup ou de um snapshot, ambos irão criar uma nova base contendo um novo endpoint.

## Encryption

A **criptografia** somente pode ser **habilitada** no **momento de criação** da base de dados.

O tipo de criptografia utilizado é através do AWS Key Management Service (KMS) utilizando o padrão de criptografia AES-256.

Importante lembrar também que uma vez ligado a criptografia, todos os níveis abaixo serão também criptografados, exemplo: automated backups, snapshots, logs e read replicas.

### How to encrypt an unencrypted instance?

Basicamente, para "ligarmos" a criptografia, devemos criar um snapshot da base, criptografá-lo e restaurar a base de dados à partir deste snapshot criptografado e pronto, já teremos nossa base criptografada.

## Tips

- O RDS possui uma feature chamada IAM Authentication e funciona com as seguintes engines: Aurora MySQl, Aurora Postgresql, MySQl, Postgresql e MariaDB.

- O RDS Automated Backups cria backups em uma única região, enquanto Snapshots e Read Replicas podem ser criados em qualquer região.

- O RDS Read Replicas Cross-Region pode eventualmente ser considerada uma ferramenta de backups por ser capaz de ser promovida a uma base própria em cenário de falha.
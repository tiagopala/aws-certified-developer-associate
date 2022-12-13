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
- **Automated Backups**

### Multi-AZ

- TODO: Explain in more details

### Read Replicas

- TODO: Explain in more details
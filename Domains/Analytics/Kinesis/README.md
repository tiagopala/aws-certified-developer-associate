# AWS Kinesis

<img height=100px; alt="kinesis_logo" src="../../../images/kinesis.png" />

<p>&nbsp;</p>

AWS Kinesis is collection of **analytics services** responsible to **collect**, **process** and **analyse streaming data**.

O Kinesis é utilizado para coletar centenas de milhares de dados que estão sendo streamados continuamente por diferentes origens simultaneamente em pequenos tamanhos, geralmente kbytes.

## Kinesis Types

### Kinesis Data Streams

Os **Data Streams** permitem a integração com aplicações customizadas para **processamento** dos dados capturados em **tempo real**. 

A arquitetura dos data streams prevê sempre um consumidor que ficará responsável por realizar o pulling nos shards para o processamento dos dados.

Ele funciona à partir da utilização de **shards**, local em que os dados são armazenados, enquanto aguardam para serem capturados por um consumidor que irá processar os dados e enviar para algum serviço como, dynamo, s3, EMR e Redshift.

O que define a capacidade de streaming é justamente o número de shards, portanto se a volumetria dos dados aumentar, para aumentar o capacidade de streaming do kinesis, você deve aumentar também o número de shards.

Cada registro possui um número sequencial que o identifica, portanto a **ordem** dos dados **sempre é mantida**.

Os **shards** possuem um p**eríodo de retenção** entre **24 horas** e **365 dias**.

Ele é dividido em dois serviços: **data streams** and **video streams**.

### Kinesis Firehose

O Firehose permite a **captura**, **transformação** e **carregamento** dos streams para análise do dados quase em tempo real através de ferramentas de BI.

Diferente do data streams, o firehose não possui shards, portanto os **dados coletados não são retidos**, porém não há necessidade de consumidores. Os dados coletados podem opcionalmente serem transformados por uma lambda e depois enviados ao S3 e após ao redshift ou somente enviados ao opensearch.

Prevê a utilização de ferramentas de BI para análise dos dados quase em tempo real.

### Kinesis Data Analytics

O Data Analytics permite a análise, querying e **transformação dos dados em tempo real através de SQL**.

Basicamente, pode utilizar o data streams ou firehose para coleta dos dados, porém utiliza queries SQL para transformação dos dados e envio ao s3, redshift ou opensearch.
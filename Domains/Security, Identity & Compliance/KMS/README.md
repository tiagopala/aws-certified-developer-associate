# AWS KMS - Key Management Service

<img height=100px; alt="kms_logo" src="../../../images/kms.png" />

<p>&nbsp;</p>

AWS KMS is a security service for **creating and managing keys** to **encrypt** and **decrypt** your data coming in or out of aws.

Serviço totalmente gerenciado, permitindo fácil integração com outros serviços da aws com apenas '*check*' para sua utilização.

## When should we use KMS?

Devemos utilizar o KMS quando nossas aplicações estão lidando com **informações sensíveis** como, dados de usuários, dados financeiros, senhas de bancos de dados, secrets ou credenciais.

## Which services easily integrates with KMS?

S3, RDS, DynamoDB, Lambda, EBS, EFS, CloudTrail, Developer Tools, entre outros.

## What is CMK?

**Customer Master Key** (CMK) atualmente chamado de **KMS keys**, pode criptografar ou descriptografar dados até 4 Kbytes. Através dele, podemos também gerar uma **Data Key** a qual não possui limitação de tamanho, podendo criptografar/descriptografar dados maiores que 4 kb.
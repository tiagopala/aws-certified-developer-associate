# AWS KMS - Key Management Service

<img height=100px; alt="kms_logo" src="../../../images/kms.png" />

<p>&nbsp;</p>

AWS KMS is a security service for **creating and managing keys** to **encrypt** and **decrypt** your data coming in or out of aws.

Serviço totalmente gerenciado, permitindo fácil integração com outros serviços da aws com apenas '*check*' para sua utilização.

## When should we use KMS?

Devemos utilizar o KMS quando nossas aplicações estão lidando com **informações sensíveis** como, dados de usuários, dados financeiros, senhas de bancos de dados, secrets ou credenciais.

## What is CMK?

**Customer Master Key** (CMK) atualmente chamado de **KMS keys**, pode criptografar ou descriptografar dados até 4 Kbytes. Através dele, podemos também gerar uma **Data Key** a qual não possui limitação de tamanho, podendo criptografar/descriptografar dados maiores que 4 kb.

### CMK Concepts

- **Alias** - Podemos criar aliases para nos referir as nossas chaves.
- **Creation Date** - Data da criação.
- **Description** - Descrição da chave.
- **Key State** - Status da chave -> enabled, disabled, pending deletione unavailable.
- **Key Material** - Material utilizado, pode ser informado pelo usuário ou pela própria aws (kms ou cloud hsm).
- **Inside AWS** - Não é possível exportar as chaves para fora do ambiente da aws.

### How to setup a CMK?

1. Informar o alias, description e key material.
2. Definir as permissões de gerenciamento da chave (Users/Roles + admin permissions).
3. Definir as permissões de usabilidade da chave (Users/Roles + usage permissions).

## Managed Keys Types

### AWS Managed Keys

São chaves criadas e gerenciadas automaticamente pela própria aws quando escolhemos utilizar a criptografia do kms em algum outro serviço.

### Customer Managed Keys

São chaves criadas e gerenciadas pelo próprio usuário.

## Most Important KMS API Calls 

- ***aws kms encrypt*** - Criptografa um texto puro em ciphertext (texto cifrado) utilizando uma customer master key.
- ***aws kms decrypt*** - Descriptografa um ciphertext que foi criptografado previamente por uma CMK em texto puro, também utiliza uma customer master key.
- ***aws kms re-encrypt*** - Descriptografa e já criptografa um arquivo criptografado. Usado quando for necessário trocar a CMK ou realizar a rotação das chaves manualmente.
- ***aws kms enable-key-rotation*** - Habilita a rotação automática das chaves.
- ***aws kms generate-data-key*** - Realização a criação de uma data key para criptografar/descriptografar arquivos maiores que 4kb.

## Which services easily integrates with KMS?

S3, RDS, DynamoDB, Lambda, EBS, EFS, CloudTrail, Developer Tools, entre outros.
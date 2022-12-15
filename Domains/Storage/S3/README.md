# Amazon S3 - Simple Storage Service

<img height=100px; alt="s3_logo" src="../../../images/s3.png" />

<p>&nbsp;</p>

Amazon S3 is a **object storage service**, that provides secure, durable and highly available objects.

Um dos diferenciais do s3, é que não temos limite de armazenamento (***unlimited storage***) e objetos individuais podem ter até 5TB.

Os arquivos são organizados dentro de **buckets**, semelhante a folders.

Os nomes dos buckets são compartilhados (**shared namespaces**), portanto devem ser únicos globamente (**globally unique**), portanto se uma pessoa já possui um bucket chamado test-bucket, você nunca conseguirá criar um bucket tendo o mesmo nome em sua conta.

> Exemplo s3 URL: https://bucket-name.s3.sa-east-1.amazonaws.com/key-name.jpg

## Components

- **Key** - Nome do objeto (arquivo).
- **Value** - Os dados que correspondem aquele objeto, geralmente um array de bytes.
- **Version ID** - Versão do objeto.
- **Metadata** - Dados dos próprios dados. Exemplo: content-type, last-modified...

## Availability & Durability

- **Disponibilidade** pode variar de acordo com o tier escolhido, entre **99.95%** e **99.99%**.

- **Durabilidade** é de **99.(11 9's)%**.

## Features

- [**Tiering/Storage Classes**](#storage-classes)
- **Lifecycle Management**
- **Versioning**

### Storage Classes

- S3 Standard
- S3 Standard-Infrequent Access
- S3 One Zone-Infrequent Access
- S3 Glacier
- S3 Glacier Deep Archive
- S3 Intelligent Tearing

#### Comparison

| Storage Class | Availability | Durability | Number AZs | Minimum Storage Time | Use Cases |
| ------------- | ------------ | ---------- | ---------- | -------------------- | --------- |
| **S3 Standard** | 99.99% | 11 9's | >= 3 | N/A | Utilizado pela maioria das aplicações |
| **S3 Standard-Infrequent Access** | 99.9% | 11 9's | >= 3 | 30 dias | Dados acessados ocasionalmente, porém entregues rapidamente quando solicitado | 
| **S3 One Zone-Infrequent Access** | **99.5%** | 11 9's | **1** | 30 dias | Aconselhável para dados não críticos acessados ocasionalmente, porém entregues rapidamente quando solicitado |
| **S3 Glacier** | 99.99% | 11 9's | >= 3 | 90 dias | Armazenamento (arquivamento) de longa duração, para dados que precisam ser acessados em minutos até horas |
| **S3 Glacier Deep Archive** | 99.99% | 11 9's | >= 3 | 180 dias | Armazenamento (arquivamento) extrema duração, para dados raramente acessados, com recuperação dos dados em até 12 horas |
| **S3 Intelligent Tearing** | 99.9% | 11 9's | >= 3 | 30 dias | Aconselhável quando desconhecemos o padrão de acesso aos dados |

## Security

Por **default**, todo novo bucket criado é **privado**. Somente o bucket owner possui permissões para subir, editar, mover e remover arquivos.

### Access Control

**Bucket Policies**

As bucket policies são **aplicadas** em **nível de bucket**, portanto se aplicam a **todos os objetos** dentro deste bucket.

> Um caso de uso, é quando desejamos compartilhar permissões de todos os arquivos do bucket para outra pessoa ou aplicação de forma simples e centralizada.

**Access Control Lists (ACL's)**

Os ACL's são aplicados a objetos individuais, podendo definir quais contas, grupos e seu respectivo nível de acesso ao arquivo. Através dos ACL's temos um controle de acesso granular, podendo conceder diferentes permissões para cada arquivo.

## Access logs

Para termos maior segurança do que está acontecendo dentro de nossos buckets, podemos habilitar o s3 access logs para logar todas as chamadas feitas para nosso bucket, sendo elas de upload, read ou delete.

> Os logs podem ficar em outro bucket, informando no momento em que estivermos habilitando esta configuração.

## Criptografia

Podemos habilitar a seguinte opção de **Server Side Encryption** e assim todos os novos arquivos já serão armazenados criptografados.

## Supported File Formats

- Photos
- Videos
- Codes
- Documents
- Text files
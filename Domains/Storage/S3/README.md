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

- **Tiering**
- **Lifecycle Management**
- **Versioning**

## Restricting access

- **Server Side Encryption** - Pode deixar a opção default habilitado e todos os novos arquivos já serão armazenados criptografados.
- **Access Control Lists (ACL's)**
- **Bucket Policies**

## Supported File Formats

- Photos
- Videos
- Codes
- Documents
- Text files
# Amazon SQS - Simple Queue Service

<img height=100px; alt="step_functions_logo" src="../../../images/sqs.png" />

<p>&nbsp;</p>

Amazon SQS is a **serverless message queueing service**, responsible for **decoupling your infrastructure**.

O SQS sempre deve ser uma opção quando é necessário **desacoplarmos** nossas aplicações.

## How SQS Works?

Devido tratar-se de uma serviço de mensageria, para funcionar depende necessariamente de um produtor e pelo menos um consumidor.

O produtor fica responsável por enviar novas mensagens a fila a qual serão recebidas e processadas pelo consumidor.

Um ponto importante para lembrarmos é que o SQS utiliza um sistema **pull-based**, para captura das mensagens, ou seja, as nossas instâncias ficarão realizando o pulling na fila do SQS para capturar novas mensagens.

![sqs-workflow](../../../images/sqs-workflow.drawio.png)
<!-- <img height=100px; alt="step_functions_logo" src="../../../images/sqs.png" /> -->

## Features

- [Visibility Timeout](#visibility-timeout)

### Visibility Timeout

Uma das principais características do SQS é a segurança no processamento de mensagens, através do **Visibility Timeout**, que é o número de tempo em segundos que a mensagem ficará invisível para outros consumidores durante seu processamento. Caso aconteça algo com o consumidor e a mensagem não consiga ser processada corretamente, a mensagem irá retornar a fila quando o tempo de visibilidade acabar.

> Importante lembrar que caso suas mensagens estejam sendo processadas mais de uma vez, uma das causas é que o tempo de processamento é inferior ao *visibility timeout*. Para resolvermos o problema devemos aumentar o tempo dado ao *visibility timeout* ou diminuir o tempo de processamento da mensagem.

## Characteristics of the messages

As mensagens tem **tamanho máximo de 256 kbytes** e podem ser enviadas nos seguintes formatos de texto: **json**, **xml** e **plaintext** (texto puro).

O período de retenção (***retention period***) **default** é de **4 dias**, porém podendo ser entre 1 minuto e **máximo** de **14 dias**.

Uma garantia que temos com o SQS é que todas as mensagens serão processadas ao menos uma vez.
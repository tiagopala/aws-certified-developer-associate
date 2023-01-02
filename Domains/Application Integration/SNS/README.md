# AWS SNS - Simple Notification Service

<img height=100px; alt="sns_logo" src="../../../images/sns.png" />

<p>&nbsp;</p>

AWS SNS is a **serverless notification service** that allows to send a message to **multiple receivers** using different formats and protocols.

O SNS é sistema **PUSH-BASED** e utiliza uma arquitetura **PUB/SUB** (**publisher/subscriber**), através dele iremos criar tópicos e nos inscrevermos neles para o recebimento das notificações.

Importante lembrar que o próprio SNS permite integração nativa com diferentes plataformas (protocolos), como por exemplo enviar um SMS ou enviar uma *push notification* para um *device*.

## Integrations

Através do SNS podemos enviar:

- Enviar **Push notifications** para diferentes dispositivos (Apple, Google, Fire OS, Windows, Android).
- Enviar **SMS** e **E-mails**.
- Integrarmos com o **SQS**.
- '*Triggar*' uma ***lambda function***.

## Internal architecture

A arquitetura interna do SNS permite disponibilidade, durabilidade, redundância e resiliência de forma nativa, através da utilização de múltiplas AZs.

## Pricing

- **Pay-as-you-go** model - "Pague o que utilizar"


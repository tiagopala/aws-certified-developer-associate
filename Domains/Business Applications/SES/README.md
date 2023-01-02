# AWS SES - Simple Email Service

<img height=100px; alt="ses_logo" src="../../../images/ses.png" />

<p>&nbsp;</p>

AWS SES is an email service designed to easily send emails to your customers at the lowest price in the market.

É um serviço de email escalável (scalable) e altamentente disponível (highly available).

Através dele podemos enviar e receber emails, sendo os emails recebidos enviados a um s3 bucket, além da possibilidade de '*triggar*' lambdas e SNS.

## Use Cases

- Automated Emails - Um novo comentário foi adicionado a sua foto.
- Online Purchases - Envio da confirmação de pagamento, pedido está sendo enviado e pedido finalizado.
- Marketing Emails - Um novo produto está disponível com desconto, entre outros.

## Differences between SES x SNS

**SES** | **SNS** |
--- | --- |
Serviço de envio de **emails (somente)** | Serviço de **pub/sub** para envio de mensagens, integração com **diferentes formatos/protocolos** |
Pode enviar e receber emails (1) | Envio para múltiplos endpoints diferentes |
Requer apenas o endereço de email de destino | Consumidores precisam se **inscrever no tópico** para receber as notificações |
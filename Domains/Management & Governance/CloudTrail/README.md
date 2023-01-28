# AWS CloudTrail

<img height=100px; alt="cloudtrail_logo" src="../../../images/cloudtrail.png" />

<p>&nbsp;</p>

AWS Cloudtrail is a **management and governance** service responsible for **recording user activity** inside and even outside aws, recording also login failed attempts.

Através dele podemos logar todas as atividades que estão acontecendo dentro da plataforma, logando tanto as chamadas de API Calls através do aws cli como também tudo que acontece através do próprio console da aws. Portanto, é possível ver qual usuário, qual operação e quando a operação foi realizada.

Para facilitar o entendimento o CloudTrail é um serviço de segurança provendo para **logs de auditoria**.

## Tips

- O CloudTrail por default consegue fazer o tracking de somente bucket level actions, para fazer o tracing de object level actions devemos habilitar o Amazon S3 data events.

- Se estivermos trabalhando com um bucket compartilhado para os registros do CloudTrail, além de sermos bucket-owner, devemos também ser object-owner para conseguirmos acessar os logs de object-level APIs.

- Para realizar o tracking de várias contas podemos criar uma Organization Trail. Member Accounts podem visualizar a Organization Trail porém não poderão alterar ou remove-la.
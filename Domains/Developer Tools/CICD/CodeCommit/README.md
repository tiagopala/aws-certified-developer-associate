# AWS CodeCommit

<img height=100px; alt="code-commit-logo" src="../../../../images/code-commit.png" />

<p>&nbsp;</p>

AWS CodeCommit is a **developer tool service** responsible to provide ***centralized code repository***.

Basicamente, como mencionado no arquivo de CI/CD, ele funciona como o próprio repositório de códigos **(git) da amazon**.

Através dele, é possível ter um trabalho colaborativo entre diversos desenvolvedores realizando alterações ao mesmo tempo no mesmo código.

Uma das principais features do CodeCommit ou de qualquer *git repository* é o versionamento do código através dos *commits* e *branches*.

> Nele, podemos armazenar nossos códigos, binários, imagens, entre outros.

## Notifications

É possível criar notificações para aberturas, atualizações e encerramentos de pull requests, comentários feitos em pull requests e quando comentários são adicionados a *commits*.

Essas notificações podem ser criadas através do uso do **SNS** em conjunto com os **CloudWatch Event Rules**.

## Tips

- As formas de se comunicar com o CodeCommit são: git credentials, ssh keys e aws access keys através do aws cli. Não é possível usar um IAM user e password.

- Os repositórios são sempre criptogrados in-transit e at rest.

- A forma mais fácil de nos conectarmos com os repositórios de forma segura é através de git credentials geradas pelo IAM e fazer as requisições através de HTTPS. 

- 
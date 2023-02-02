# Amazon ECS - Elastic Container Registry

<img height=100px; alt="ecr_logo" src="../../../images/ecr.png" />

<p>&nbsp;</p>

O Amazon ECS é um serviço de containers totalmente gerenciado a qual disponibiliza um registro de docker images na própria aws.

## Tips

- Para conseguirmos realizar o docker pull de uma imagem presente em nosso ECR, não é possível utilizar o docker login, devemos utilizar as próprias APIs do ECR através do AWS CLI e depois realizar o docker pull normalmente.
    > $(aws ecr get-login --no-include-email) = Comando para realizar login no ECR
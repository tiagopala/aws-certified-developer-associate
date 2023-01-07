# Amazon ECS - Elastic Container Service

<img height=100px; alt="ecs_logo" src="../../../images/ecs.png" />

<p>&nbsp;</p>

Amazon ECS is a **container service** used to **deploy, manage, scale and orchestrate** containers.

O ECS é muito similiar ao *kubernetes*, porém é a própria ferramenta da amazon para orquestração de containers (docker linux / windows containers), já possuindo integração nativa com alguns serviços, como: *elastic load balancer* (elb), *ec2 security groups*, *elastic block store* (ebs) *volumes* e *IAM roles*.

O ECS utiliza o ECR (Elastic Container Registry) para armazenamento das imagens utilizadas no processo de *deploy* dos containers.

## Task Definitions Types

Atualmente podemos executar nossos containers utilizando instâncias **ec2** ou instâncias **fargate**.

Se o objetivo é possuir maior controle sobre a instalação, configuração e gerenciamento do ambiente devemos utilizar instâncias ec2. Porém, podemos utilizar as instâncias do tipo **fargate** pois são **serverless**, não tendo que gerenciar toda essa infraestrutura, deixando esta responsabilidade para a amazon.
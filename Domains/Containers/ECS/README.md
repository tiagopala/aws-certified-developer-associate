# Amazon ECS - Elastic Container Service

<img height=100px; alt="ecs_logo" src="../../../images/ecs.png" />

<p>&nbsp;</p>

Amazon ECS is a **container service** used to **deploy, manage, scale and orchestrate** containers.

O ECS é muito similiar ao *kubernetes*, porém é a própria ferramenta da amazon para orquestração de containers (docker linux / windows containers), já possuindo integração nativa com alguns serviços, como: *elastic load balancer* (elb), *ec2 security groups*, *elastic block store* (ebs) *volumes* e *IAM roles*.

O ECS utiliza o ECR (Elastic Container Registry) para armazenamento das imagens utilizadas no processo de *deploy* dos containers.

## Task Definitions Types

Atualmente podemos executar nossos containers utilizando instâncias **ec2** ou instâncias **fargate**.

Se o objetivo é possuir maior controle sobre a instalação, configuração e gerenciamento do ambiente devemos utilizar instâncias ec2. Porém, podemos utilizar as instâncias do tipo **fargate** pois são **serverless**, não tendo que gerenciar toda essa infraestrutura, deixando esta responsabilidade para a amazon.

## AWS Docs for containers and microservices

- [Running Containerized Microservices on AWS (pdf)](https://d1.awsstatic.com/whitepapers/DevOps/running-containerized-microservices-on-aws.pdf)
- [The Twelve Factors](https://12factor.net/) - *Metholody for building sas apps*

## Tips

- Terminar instâncias que estão com status igual a STOPPED impactará em synchronization issues, fazendo com que o container não seja removido do cluster automaticamente.

- A role responsável por dar permissão aos PODs no ECS é a task execution role e deve ser 'attachada' na task.

- Para escalarmos as PODs (tasks) dentro de um cluster ECS, podemos usar target tracking policies para métricas pré definidas pelos recursos, por exemplo, do Auto Scaling Group ou Application Load Balancer.

- Caso desejarmos escalar nossos PODs (tasks) com base em algum parâmetro de nossa base de dados, quantidade de requisições por segundo na aplicação ou por exemplo na quantidade de mensagens disponíveis em nossas filas, devemos criar uma CloudWatch Custom Metric, criar um Alarm à partir desta métrica e utilizar este alarme como um target em nosso Auto Scaling Group para nossas instâncias EC2.

- 
# Amazon EC2 - Elastic Compute Cloud

<img height=100px; alt="ec2_logo" src="../../../images/ec2.svg" />

<p>&nbsp;</p>

EC2 is a **Compute Service** responsible for provision **secure and resizable compute capacity** in the cloud within minutes.

*"In another words"*, é semelhante a uma Virtual Machine (VM), porém hospedada na nuvem nos próprios data centers da aws.

## Differential advantages

Um dos diferenciais do EC2 é principalmente a sua capacidade de escalar para cima ou para baixo os seus recursos quando necessário.

Outro diferencial notável é ter a possibilidade de termos novos servidores rodando em minutes. 

## Payment Model

**<em>"Pay as you go"</em>** model - Você paga somente a capacidade computacional que você usar.

### Instance Pricing Options

- **On Demand** - Pagar pela hora ou segundo dependendo do tipo de instância.
- **Reserved** - Reservar capacidade de 1 a 3 anos, tendo descontos até 72% no valor da hora.
- **Spot** - Comprar capacidade não utilizada pela amazon até o presente momento por um preço inferior. Preço flutua de acordo com a quantidade disponível e demanda.
- **Dedicated** - Comprar servidores EC2 físicos.

#### On Demand

- **Flexibility** - Subir instâncias a qualquer momento por uma preço fixo.
- **Short-Term** - Sem pagamento antecipado ou compromissos/contratos de longo prazo. Aconselhável para aplicações com tempo de uso curto, *spikes* ou aplicações com workload imprevisível.
- **<em>Testing the water</em>** - Aplicações sendo desenvolvidas pela primeira vez.

#### Reserved

- **Predictable Usage** - Aplicações estáveis ou com uso previsível.
- **Specific Capacity Required** - Aplicações que requerem uma capacidade específica.
- **Pay Up-Front** - Pagamento adiantado para reduzir custos (descontos).

    Types:

    - **Standard RIs** - Não é possível alterar o tipo de instância contratado.
    - **Convertible RIs** - É possível alterar o tipo de instância de preço igual ou maior.
    - **Scheduled RIs** - Quando o horário de execução da aplicação é previsível.

#### Spot

- **Flexible start and end times** - Aplicações devem possuir um tempo de início e finalização flexíveis, pois o preço da instância pode subir e suas instâncias spot podem ser finalizas.
- **Cost Sensitive** - Aplicações que só valem a pena se o custo for extremamente baixo.
- **Urgent Capacity** - Aplicações que requerem uma grande capacidade adicional.

#### Dedicated Hosts

- **Compliance** - Quando é necessário respeitarmos requisitos regulatórios.
- **Licensing** - Quando é necessário respeitarmos licenças que não suportam multi-tenancy.

    Types:

    - **On Demand**
    - **Reserved**

> Pode ser usado em conjunto com o [Saving Plans](../../AWS%20Cost%20Management/AWS%20Cost%20Explorer/README.md#saving-plans)

## Instance Types

O tipo de instância determina o tipo de hardware do host que a aplicação irá ser hospedada.

Para o exame, devemos lembrar que cada tipo de instância oferece uma capacidade diferente, como poder computacional (compute), memória (memory) e armazenamento (storage).

Importante lembrar que o agrupamento dessas instências é realizado em famílias de capacidades.

## Storage

- [EBS](./EBS/README.md)

## Load Balancing

- [ELB](./ELB/README.md)

## Tips

### EC2

- Os scripts informados no User Data são executados somente uma única vez no momento em que a instância for provisionada.
    > Os scripts são executados com *root level permissions*.

- Para consultar o public IP e private IP de uma instância devemos fazer um CURL no seguinte URI: 169.254.169.254/latest/metadata.

- Instâncias do tipo "burstable performance" são desenhadas para terem uma linha base de performance de CPU, porém pode aumentar para um pico caso necessário. Nos primeiros 12 meses não haverá custo adicional sobre o tempo em que a instância utilizou este "crédito adicional".

- As opções válidas para uma Spot Instance quando ela for finalizada devido seu aumento de preço são: Stop, Terminate ou Hibernate.

- Caso reservarmos uma instância por um tempo determinado e passarmos deste tempo, tempos adicionais em que não foram reservados serão cobrados como OnDemand.

- Se quisermos prover uma reserva de capacidade devemos utilizar Zonal Reserved Instances pois Regional Reserved Instances não provêm reserva de capacidade.

- Se quisermos habilitar o monitoramento detalhado para instâncias que já estão rodando devemos usar o seguinte comando: ```aws ec2 monitor-instances --instance-ids <value>```, para subir novas instâncias já com monitoramento detalhado: ```aws ec2 run-instances --image-id <value> --monitoring Enabled=true```.

- Tanto Dedicated Instances quanto Dedicated Hosts são single-tenant, porém o dedicated hosts podem ser usados quando tivermos licenças e ainda podemos ver aonde os recursos estão locados em detrimento de serem um pouco mais custosos que as dedicated instances.

### Auto Scaling Groups

- Para configurarmos um Auto Scaling Group devemos informar o AMI ID e instance type no launch template.

- ASG não podem provisionar instâncias entre regiões (ASG can't "spam" across regions).

- ASG podem podem provisionar instâncias em 1 ou mais AZ's (AGS can "spam" across AZ's at the same region).

- Caso uma AZ em que tenhamos instâncias provisionadas pelo ASG fique fora do ar, o próprio ASG se encarrega de provisionar essas instâncias em outra AZ com o objetivo de manter a mesma quantidade de instâncias necessário.

- Para ASG's dentro de uma VPC, as instâncias serão provisionadas dentro de subnets.

- Se a configuração de um ASG for feito pelo AWS Console ele irá por default com basic monitoring. Porém, se for realizado através do AWS CLI ou AWS SDK, por default ele virá com monitoramento detalhado.

- Um ASG sempre respeita a capacidade máxima estipulada no processo de scaling.

- ASG possuem um processo periódico para verificação de health checks, caso uma instância esteja unhealthy, ele irá terminar a instância e subir uma nova instância no lugar.

### Elastic Load Balancer

- Um dos focos do ELB é a disponibilidade (availability) visto que um dos seus papéis é verificar constantemente os health checks e distribuir o tráfego para os nós que estiverem "de pé".

- O tráfego interno entre os Load Balancers e instâncias é feito através de IP's privados.

- Os Target Groups de um ELB podem ser apenas instâncias na mesma região.

- Classic Load Balancers distribuem o tráfego de forma inconsistente entre as instâncias de tipos diferentes optando sempre por instâncias que possuem maior capacidade.

- Os tipos de roteamento a partir de rotas são: Path Based (example.com/api) e Host Based (api.example.com).

- O Application Load Balancer permite os seguintes targets: Instance, IP e Lambda.

- O ALB não permite especificarmos o roteamento utilizando-se de IPs públicos, devemos sempre utilizar blocos CIDR.

- Para o ALB, se estivermos usando IPs como target, podemos rotear o tráfego para qualquer endereço de IP privado de 1 ou mais Network Interfaces.

- Se tivermos um ELB em nossa arquitetura, os seguintes erros representam:
  - 503 Service Unavailable: Esquecemos de registrar os target groups.
  - 504 Gateway Timeout: Provavelmente corresponde a um server side problem, pois a origem não respondeu no tempo previsto.

- A TLS Termination é o termo utilizado quando temos uma comunicação segura e criptografada através do HTTPS. Se a TLS Termination estiver no ELB, a comunicação entre o cliente e o load balancer será criptografada, porém se quisermos ter uma comunicação segura de ponta a ponta devemos criar um secure listener e configurar nossa aplicação (instância ec2) para usar uma porta segura (443).

- O ALB sempre vem com o Cross-Zone load balancing habilitado por default.

- Sempre que o objetivo for performance devemos escolher o Network Load Balancer (NLB).

- Para descobrirmos incoming requests e latências provenientes do ALB devemos consultar os ALB access logs.

### Security Groups

- Caso nossa instância EC2 seja um web server exposto para a internet, porém nossos usuários estão recebendo timeouts, pode significar um problema na configuração dos security groups.

- EC2 Security Groups são stateful, portanto habilitar uma inbound port automaticamente também habilita uma outbound port.
    > VPC Network ACL's são stateless, portanto devemos habilitar tanto inbound quanto outbound ports.

### EBS Volumes

- Se desejarmos compartilhar um EBS Volume com outra conta, podemos criar um snapshot, conceder as permissões necessárias para outra conta e compartilhá-lo.

- EBS Volumes são AZ locked, ou seja, só podemos 'attachar' instâncias da mesma região em nosso EBS volume.

- EBS Volumes possuem suporte tanto para in-flight quanto encryption at rest.

- Para aumentarmos a performance de um EBS Volume devemos:
    1. Colocar os volumes juntos no Raid 0.
    2. Garantir que o tipo de instância utilizado pode ser otimizado.
    3. Nunca planejar snapshots durante momentos de grande utilização da plataforma pois snapshots impactam na performance.

- Sobre o tipo de volume Provisioned IOPS, a proporção entre o Provisioned IOPS pelo requested volume size é de 50:1. Portanto se tivermos um volume de 200 Gb, teremos no máximo 10.000 IOPS. (200 x 50).

### Elastic IPs

- Serviços de DNS são identificados a partir de IPs, portanto podemos criar um Elastic IP para mascarar a falha de uma instância ou software remapeando rapidamente para o endereço de IP de outra instâsncia.
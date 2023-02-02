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

- Caso desejarmos alterar o comportamento do atributo 

### Auto Scaling Groups

- Para configurarmos um Auto Scaling Group devemos informar o AMI ID e instance type no launch template.

- ASG não podem provisionar instâncias entre regiões (ASG can't "spam" across regions).

- ASG podem podem provisionar instâncias em 1 ou mais AZ's (AGS can "spam" across AZ's at the same region).

- Caso uma AZ em que tenhamos instâncias provisionadas pelo ASG fique fora do ar, o próprio ASG se encarrega de provisionar essas instâncias em outra AZ com o objetivo de manter a mesma quantidade de instâncias necessário.

- Para ASG's dentro de uma VPC, as instâncias serão provisionadas dentro de subnets.

- Se a configuração de um ASG for feito pelo AWS Console ele irá por default com basic monitoring. Porém, se for realizado através do AWS CLI ou AWS SDK, por default ele virá com monitoramento detalhado.

- Um ASG sempre respeita a capacidade máxima estipulada no processo de scaling.

- ASG possuem um processo periódico para verificação de health checks, caso uma instância esteja unhealthy, ele irá terminar a instância e subir uma nova instância no lugar.

### Security Groups

- Caso nossa instância EC2 seja um web server exposto para a internet, porém nossos usuários estão recebendo timeouts, pode significar um problema na configuração dos security groups.

- EC2 Security Groups são stateful, portanto habilitar uma inbound port automaticamente também habilita uma outbound port.
    > VPC Network ACL's são stateless, portanto devemos habilitar tanto inbound quanto outbound ports.

### Elastic IPs

- Serviços de DNS são identificados a partir de IPs, portanto podemos criar um Elastic IP para mascarar a falha de uma instância ou software remapeando rapidamente para o endereço de IP de outra instâsncia.
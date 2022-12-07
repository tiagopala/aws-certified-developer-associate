# EC2 - Elastic Compute Cloud

<img height=100px; alt="iam_logo" src="../../../images/ec2.svg" />

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
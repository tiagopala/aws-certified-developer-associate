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

- **Flexibility**
- **Short-Term** - Sem pagamento antecipado ou compromissos/contratos de longo prazo. Aconselhável para aplicações com tempo de uso curto, *spikes* ou aplicações com workload imprevisível.
- **<em>Testing the water</em>** - Aplicações sendo desenvolvidas pela primeira vez.

#### Reserved

- **Predictable Usage**
- **Specific Capacity Required**
- **Pay Up-Front**

Reserved Instances Types:

- **Standard RIs**
- **Convertible RIs**
- **Scheduled RIs**
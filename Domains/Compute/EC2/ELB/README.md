# ELB - Elastic Load Balancer

<img height=100px; alt="iam_logo" src="../../../../images/elb.svg" />

<p>&nbsp;</p>

ELB is an EC2 feature responsible for automatically distribute incoming application traffic across multiple targets and virtual appliances in one or more AZs.

<div align="center">
    <img height=300px; alt="elb_workflow_visualization" src="../../../../images/elb.drawio.png" />
</div>

## Types

- [**Application Load Balancer**](./README.md#application-load-balancer-alb) - ALB
- [**Network Load Balancer**](./README.md#network-load-balancer-nlb) - NLB
- [**Gateway Load Balancer**](./README.md#gateway-load-balancer-glb) - GLB
- [**Classic Load Balancer**](./README.md#classic-load-balancer-clb) (legacy)

### Application Load Balancer (ALB)

Realiza o balanceamanto de carga através das portas 80 (HTTP) and 443 (HTTPS). É considerado um balanceamento inteligente visto que ele pode capturar informações da aplicação e criar requisições avançadas e customizadas durante o balanceamento dos workloads devido o balanceamento ocorrer na camada 7 (application).

### Network Load Balancer (NLB)

O balancemanto de carga é realizado através dos protocolos TCP/UDP, operando na camada 4 (transport) sendo o balanceamento mais performático por estar em nível de conexão. Deve ser usado por aplicações em que a performance é de extrema importância.

### Gateway Load Balancer (GLB)

Permite o balanceamento de carga de aplicações de terceiros, como aplicações compradas no marketplace, virtual firewalls de companhias como Fortnet, Palo Alto, Juniper e Cisco, além de sistemas IDS/IPS de empresas como CheckPoint, Trend Micro, entre outras.

### Classic Load Balancer (CLB)

É o tipo mais antigo, podendo realizar o balanceamento em ambas camadas, porém não é possível criar regras customizadas e nem atingir o mesmo tipo de performance do NLB.
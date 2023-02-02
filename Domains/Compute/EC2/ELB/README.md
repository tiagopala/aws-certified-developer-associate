# ELB - Elastic Load Balancer

<img height=100px; alt="iam_logo" src="../../../../images/elb.svg" />

<p>&nbsp;</p>

ELB is an EC2 feature responsible for automatically distribute incoming application traffic across multiple targets and virtual appliances in one or more AZs.

<div align="center">
    <img height=400px; alt="elb_workflow_visualization" src="../../../../images/elb.drawio.png" />
</div>

## Types

- [**Application Load Balancer**](./README.md#application-load-balancer-alb) - ALB
- [**Network Load Balancer**](./README.md#network-load-balancer-nlb) - NLB
- [**Gateway Load Balancer**](./README.md#gateway-load-balancer-glb) - GLB
- [**Classic Load Balancer**](./README.md#classic-load-balancer-clb) (legacy)

### OSI Layers

<img height="400px" alt="iam_logo" src="../../../../images/osi-layers.png" />

### Application Load Balancer (ALB)

Realiza o balanceamanto de carga através das portas 80 (HTTP) and 443 (HTTPS). É considerado um balanceamento inteligente visto que ele pode capturar informações da aplicação (digamos que ela é *"application aware"*) e criar requisições de roteamento avançadas/customizadas utilizando inclusive paramêtros do cabeçalho da requisição (*HTTP headers*) durante o balanceamento dos workloads devido o balanceamento ocorrer na camada 7 (application).

<div align="center">
    <img width=500px; alt="elb_workflow_visualization" src="../../../../images/alb.drawio.png" />
</div>

### Network Load Balancer (NLB)

O balancemanto de carga é realizado através dos protocolos TCP/UDP, operando na camada 4 (*transport*) sendo o balanceamento mais performático, capaz de lidar com milhões de requisições por segundo. Deve ser usado por aplicações em que a performance é de extrema importância, visto que ele possui o maior preço também.

### Gateway Load Balancer (GLB)

Permite o balanceamento de carga de aplicações de terceiros, como aplicações compradas no marketplace, virtual firewalls de companhias como Fortnet, Palo Alto, Juniper e Cisco, além de sistemas IDS/IPS de empresas como CheckPoint, Trend Micro, entre outras.

### Classic Load Balancer (CLB)

É o tipo mais antigo, podendo realizar o balanceamento em ambas camadas (4 e 7), porém não é possível criar regras de roteamento customizadas igual ao ALB e nem atingir o mesmo tipo de performance do NLB.

Features
- X-Forwarded-For headers
- Sticky sessions

**X-Forwarded-For Headers**

É uma feature que permite que identificarmos o IP de origem de uma requisição após ela ser roteada através de um load balancer, incluindo o valor do ip de origem dentro do header, para ser capturado pelo web server.

> Feature disponível apenas para o Application Load Balancer e Classic Load Balancer

<div align="center">
    <img width="500px" alt="elb_workflow_visualization" src="../../../../images/clb.drawio.png" />
</div>

## Common ELB Errors

### 504 - Gateway Timeout

Geralmente este erro ocorre quando o load balancer não consegue estabelecer a conexão com o target, sendo ele um web server, uma base de dados ou uma lambda. Indica geralmente que a aplicação está com problemas ou até fora do ar.

## Tips

- Um dos focos do ELB é a disponibilidade (availability) visto que um dos seus papéis é verificar constantemente os health checks e distribuir o tráfego para os nós que estiverem "de pé".

- O tráfego interno entre os Load Balancers e instâncias é feito através de IP's privados.

- Os Target Groups de um ELB podem ser apenas instâncias na mesma região.

- Se tivermos um ELB em nossa arquitetura, os seguintes erros representam:
  - 503 Service Unavailable: Esquecemos de registrar os target groups.
  - 504 Gateway Timeout: Provavelmente corresponde a um server side problem, pois a origem não respondeu no tempo previsto.

- A TLS Termination é o termo utilizado quando temos uma comunicação segura e criptografada através do HTTPS. Se a TLS Termination estiver no ELB, a comunicação entre o cliente e o load balancer será criptografada, porém se quisermos ter uma comunicação segura de ponta a ponta devemos criar um secure listener e configurar nossa aplicação (instância ec2) para usar uma porta segura (443).

- Assim como o Route53 pode ser usado para distribuição de tráfego.

## Application Load Balancer

- Os tipos de roteamento a partir de rotas são: Path Based (example.com/api) e Host Based (api.example.com).

- O Application Load Balancer permite os seguintes targets: Instance, IP e Lambda.

- Para o ALB, se estivermos usando IPs como target, podemos rotear o tráfego para qualquer endereço de IP privado de 1 ou mais Network Interfaces.

- O ALB não permite especificarmos o roteamento utilizando-se de IPs públicos, devemos sempre utilizar blocos CIDR.

- O ALB sempre vem com o Cross-Zone load balancing habilitado por default.

- Para descobrirmos incoming requests e latências provenientes do ALB devemos consultar os ALB access logs.

## Network Load Balancer

- Sempre que o objetivo for performance devemos escolher o Network Load Balancer (NLB).

## Classic Load Balancer

- Classic Load Balancers distribuem o tráfego de forma inconsistente entre as instâncias de tipos diferentes optando sempre por instâncias que possuem maior capacidade.
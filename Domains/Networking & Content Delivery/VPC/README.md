# Amazon VPC - Virtual Private Cloud

<img height=100px; alt="vpc_logo" src="../../../images/vpc.png" />

<p>&nbsp;</p>

É um serviço para criação e gerenciamento de sua própria rede virtual na nuvem.

## Tips

### Network ACL (Access Control List)

- VPC Network ACL's são stateless, portanto devemos habilitar tanto inbound quanto outbound ports.

- Se tivermos uma aplicação web que seja consumida pela internet e tenha um Network ACL em frente, devemos habilitar as ephemeral ports (1024 - 65535) para que a aplicação consiga ser consumida corretamente.

### Gateway Endpoints

- Se em nossa VPC tivermos uma private subnet em que precisamos nos conectar com o DynamoDb ou S3 sem sair da rede private devemos criar um gateway endpoint para cada serviço e cadastrá-los em nosso route table.


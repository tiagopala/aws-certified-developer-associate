# IAM - Identity Access Management

<img height=100px; alt="iam_logo" src="../../../images/IAM_logo.png" />

<p>&nbsp;</p>

IAM is an AWS **Universal Service** responsible for user management and their level of access to the AWS Console.

- **Centralized** (Controle centralizado da conta)
- **Access** (Compartilhar acesso a conta)
- **Permissions** (Concessão de permissões granulares de acesso a conta)
- **Identity Federation** (Suporte a integração de identity providers como Google, Facebook...)

## Features

- Multi-Factor Authentication
- Temporary Access (principalmente ao acesso de arquivos temporários do s3)
- Password Policies (rotation policies - políticas de rotação de senhas)
- AWS Services Integrations
- Compliance (suporte a PCI DSS - meios de pagamento)

## Divided In

- **Users**: Pessoas
- **Groups**: Conjunto de usuários/pessoas
- **Roles**: Attach de uma "Função" para conceder um conjunto de permissões
- **Policies**: Concessão de uma permissão específica (JSON)

> Users has not permissions when first created. Permissions need to be granted.

## Access Types

- **Console**
- **Programmatic Access** - Necessário para utilização do AWS CLI, SDKs e API calls

## Tools

### Policy Simulator

Serviço de simulação de policies em tempo real.

Link do serviço: [policysim.aws.amazon.com](https://policysim.aws.amazon.com/home/index.jsp).

#### Using Scenarios

- Verificar se determinada policy possui acesso a uma determinada ação de um serviço específico.
- Auxiliar no troubleshooting quando suspeitamos que é um problema de acesso.

> Exemplo: A imagem abaixo verifica se o grupo `adminGroup` possui acesso para `listar tabelas` no `DynamoDb`.

![iam policy simulator](../../../images/aws_iam_policy_simulator.png)

### Policy Generator

Serviço para criação de policies (conceder permissões)

Link do serviço: [awspolicygen.s3.amazonaws.com](https://awspolicygen.s3.amazonaws.com/policygen.html)

## Best Practices

Quando for conceder acesso a serviços, sempre opte por ***roles*** e ***policies*** com os menores níveis de acesso necessários, pois são a opção mais segura, dessa forma não é necessário utilizar as credenciais - *access key id* e *secret access key* - *hard coded* dentro de suas instâncias ec2, por exemplo.

## Tips

- Alterações em policies que estão *'attached'* a uma role são aplicadas instantâneamente.

- Podemos '*attach*' ou '*detach*' roles sem pararmos (stop) ou terminarmos nossas instâncias. Esta operação pode ser feita com a instância em execução.
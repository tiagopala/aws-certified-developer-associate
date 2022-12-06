# IAM - Identity Access Management

<img height=100px; src="../../../images/IAM_logo.png" />

AWS Service responsible for user management and their level of access to the AWS Console.

- Centralized (Controle centralizado da conta)
- Access (Compartilhar acesso a conta)
- Permissions (Concessão de permissões granulares de acesso a conta)
- Identity Federation (Suporte a integração de identity providers como Google, Facebook...)

## Features

- Multi-Factor Authentication
- Temporary Access (principalmente ao acesso de arquivos temporários do s3)
- Password Policies (rotation policies - políticas de rotação de senhas)
- AWS Services Integrations
- Compliance (suporte a PCI DSS - meios de pagamento)

## Divided In

- Users: Pessoas
- Groups: Conjunto de usuários/pessoas
- Roles: Attach de uma "Função" para conceder um conjunto de permissões
- Policies: Concessão de uma permissão específica (JSON)
# AWS CLI 

<img height=100px; alt="aws_cli" src="../images/aws-cli.png" />

<p>&nbsp;</p>

O AWS CLI (command line interface) é uma ferramenta da aws que possibilita o gerenciamento de nossa conta assim como de nossos recursos de forma unificada. Através dele podemos criar, alterar e remover recursos utilizando o próprio cli, além de automatizar operações através de scripts.

> Atualmente AWS CLI é compatível com os seguintes sistemas operacionais: Windows, Linux and MAC.

## Pagination

Caso o resultado de alguma operação envolvendo o CLI retorne um erro de *Timed Out*, pode-se imaginar que é devido a quantidade de informações solicitadas pelo comando.

Temos algumas formas de resolver o problema, a primeira é a utilização do paramêtro ```--page-size``` e a segunda é definindo um valor máximo a ser retornado na operação através do paramêtro ```--max-items```.

### Page Size

```aws s3api list-objects --bucket BucketName --page-size 100```

Utilizando o comando acima com o paramêtro de paginação, ele irá sobrescrever o valor default de 1000 para o valor informado pelo usuário (100), irá realizar múltiplas (10) chamadas em background, capturar os retornos e mostrar o resultado da operação solicitada.

### Max Items

```aws s3api list-objects --bucket BucketName --max-items 100```

Já utilizando o paramêtro --max-items, estamos definindo o valor máximo de itens a serem retornados, assim ele irá apenas retornar os primeiros itens de acordo com a quantidade informada pelo usuário (10).

## Best practices

- **Least Privilege** - Sempre de o mínimo acesso necessário.
- **Use Groups** - Utilize grupos para gerenciamento de permissões e adicione os usuários necessitam herdar as permissões necessárias para aquele grupo.
- **Private Key Pairs** - Cada desenvolvedor deverá ter sua própria key pair.

## Remember

Lembre-se que a visualização da sua Secret Access Key é única, em caso de perda, você deverá criar uma nova.
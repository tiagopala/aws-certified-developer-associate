# AWS CodeDeploy

<img height=100px; alt="code-deploy-logo" src="../../../../images/code-deploy.png" />

<p>&nbsp;</p>

AWS CodeDeploy is a developer tool service responsible to automated the deployment of new versions of your code to your production environment.

Através do CodeDeploy, podemos automatizar todo o fluxo de deployment para os nossos ambientes em especial para o ambiente de produção.

## Deployment Types and their peculiarities

### In-Place Deployment

O *In-Place deployment* prevê a conservação de cada instância que está no ar, pois ele irá remover momentaneamente o POD do load balancer durante o processo de download e deploy do novo código nesta mesma instância. Após o novo código ser *deployado*, esta instância será adicionada novamente ao load balancer para ser consumida. O que acaba implicando em capacidade reduzida durante o processo de *deployment*, pois sempre uma instância estará "fora do ar" para baixar a nova versão.

Caso o novo código esteja com problemas e tenha a necessidade de se realizar um *roll back*, é necessário fazer o deploy novamente da antiga versão em cada POD, implica novamente em capacidade reduzida.

![code-deploy-in-place-deployment](../../../../images/code-deploy-in-place-deployment.drawio.png)

### Blue/Green Deployment

O *Blue Green deployment* prediz que continuaremos com os antigos PODs que estão com a versão antiga por um tempo (blue), enquanto verificamos que o novo código está OK. Enquanto subimos novos PODs com a nova versão e apenas apontamos para eles. Dessa forma, não possuímos capacidade reduzida e em caso de roll back, basta apontarmos o load balancer para as antigas instâncias e pronto.

> Apesar dos benefícios, importante lembrar que teremos 2 ambientes coexistindo, rodando lado a lado, enquanto validamos a nova versão. Implicando em maiores custos.

![code-deploy-blue-green-deployment](../../../../images/code-deploy-blue-green-deployment.drawio.png)

#### Comparisons

**In-Place** | **Blue/Green** |
------------ | -------------- |
**Capacidade reduzida** durante deployment | **Sem redução** na capacidade |
Não possui suporte para lambdas | Possui suporte para lambdas |
***Roll back*** prevê ***re-deploy*** | Apenas **apontar** para o ***environment*** desejado, não requer '*re-deploy*' |
Deve ser usado para o primeiro *deploy* de suas peças | Não é aconselhável em ambientes produtivos |
Preço se mantém | **Custos adicionais** por ter 2 *environments* rodando lado a lado |
# Amazon Cloudfront

<img height=100px; alt="cloudfront_logo" src="../../../images/cloudfront.png" />

<p>&nbsp;</p>

Cloudfront is Amazon's own **Content Delivery Network (CDN)**.

Em outras palavras, é um sistema de servidores distribuídos para entrega de páginas ou qualquer outro conteúdo da internet, como vídeos, fotos e assim por diante.

## How Cloudfront works and why should i use it?

Basicamente, o cloudfront permite a **entrega de conteúdo** de forma mais **performática por todo o globo** através do uso dos Edge Locations e da própria rede interna da Amazon (Amazon's  backbone network), assim aonde quer que o usuário esteja, ele estará consumindo o conteúdo através do edge location mais próximo, não sendo necessário se comunicar com a origem do conteúdo.

### Workflow

![cloudfront-workflow](../../../images/cloudfront-workflow.png)

Como pode ser visto acima, o usuário não está consumindo o conteúdo direto da origem, mas sim do edge location mais próximo, melhorando a experiência e performance do serviço.

## TTL (Time To Live)

O nome dado ao tempo em que o conteúdo fica cacheado é **TTL** e o valor é de **24 horas**.

> Importante lembrar que caso necessário, é possível invalidar o conteúdo (atualizar o conteúdo *'cacheado'*), porém você será cobrado por isto.

## Origin Access Identity

Caso seja interessante **restringir acesso** somente pelo endpoint do **cloudfront**, podemos criar um ***Origin Access Identity*** que é basicamente um **usuário especial do cloudfront** com permissão de leitura em nossa origem e remover o acesso público da nossa origem na internet.

Exemplo: Caso tenhamos uma imagem em nosso bucket exposta na internet, podemos criar uma distruição do cloudfront, criar um OAI, atualizar as buckets policies - processo realizado automaticamente pelo cloudfront - e bloquear o acesso ao bucket pela internet. Assim, somente requisições provenientes de nosso cloudfront irão conseguir consumir a imagem, não sendo mais possível visulizá-la diretamente através do endpoint do próprio s3.

## Terminology

- **Cloudfront Edge Location** - Local (físico) aonde o conteúdo será cacheado.
- **Cloudfront Origin** - Origem (fonte), pode ser: **s3 bucket**, **ec2 instance**, **elb**, **route 53** ou até um web server próprio.
- **Cloudfront Distribution** - Nome da configuração dá distruição de conteúdo já configurada.
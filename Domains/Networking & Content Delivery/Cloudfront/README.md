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

## Allowed Methods

Os Cloudfront Allowed Methods basicamente é uma configuração para **definir as características** da sua **distribuição** do cloudfront. 

Por exemplo, imagine que seu site seja apenas um blog pessoal, em que seus usuários apenas consumirão o conteúdo presente. Neste caso, podemos liberar apenas os métodos HTTP GET, HEAD e OPTIONS. Porém, imagine agora que você possui um e-commerce, em que seus usuários irão interagir com os produtos através da criação de listas de consumo, adição de itens ao carrinho de compras e finalização de uma compra, todos as ações comentadas anteriormente são interativas portanto os métodos POST, PUT, PATCH e DELETE também serão necessários.

**To Remember**

- **Read-only** website: **GET**, **HEAD**, **OPTIONS**
- **Interactive** website: **POST**, **PUT**, **PATCH**, **DELETE**

## Origin Access Identity

Caso seja interessante **restringir acesso** somente pelo endpoint do **cloudfront**, podemos criar um ***Origin Access Identity*** que é basicamente um **usuário especial do cloudfront** com permissão de leitura em nossa origem e remover o acesso público da nossa origem na internet.

Por exemplo, caso tenhamos uma imagem em nosso bucket exposta na internet, podemos criar uma distruição do cloudfront, criar um OAI, atualizar as buckets policies - processo realizado automaticamente pelo cloudfront - e bloquear o acesso ao bucket pela internet. Assim, somente requisições provenientes de nosso cloudfront irão conseguir consumir a imagem, não sendo mais possível visulizá-la diretamente através do endpoint do próprio s3.

## Terminology

- **Cloudfront Edge Location** - Local (físico) aonde o conteúdo será cacheado.
- **Cloudfront Origin** - Origem (fonte), pode ser: **s3 bucket**, **ec2 instance**, **elb**, **route 53** ou até um web server próprio.
- **Cloudfront Distribution** - Nome da configuração dá distruição de conteúdo já configurada.

## Tips

- Um dos protocolos disponibilizados pelo CloudFront é o Viewer Protocol Policy.

- Se o CloudFront retornou um HTTP Status Code 504 (gateway timeout), provavelmente indica um server side problem, pois a origem não conseguiu responder no tempo esperado.

- No CloudFront, quando estamos criando Signed URL's, a publicy key fica com o CloudFront enquanto a private key é usada em parte da URL gerada. Quando estamos usando a root account para gerenciar as CloudFront keys podemos ter somente até 2 key pairs por conta, porém se estivermos usando o CloudFront key groups, podemos associar um número maior de chaves.

- CloudFront permite uma conexão segura tanto com o client quanto com o backend, ou seja, tanto client-side quanto server-side.

- CloudFront pode servir tanto conteúdos estáticos quanto dinâmicos com baixa latência para usuários globalmente com múltiplas origens.

- Os recursos interativos do CloudFront também inclui o HTTP Method Delete.
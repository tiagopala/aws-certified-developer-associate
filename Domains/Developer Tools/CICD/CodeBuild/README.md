# AWS CodeBuild

<img height=100px; alt="code-build-logo" src="../../../../images/code-build.png" />

<p>&nbsp;</p>

## Tips

- A configuração do CodeBuild é realiada pelo arquivo buildspec.yml junto aos CodeBuild environments.

- O CodeBuild possui uma feature nativa para lidar com timeouts, basta habilitar o CodeBuild Timeouts.

- É um serviço totalmente gerenciado pela aws, portanto não precisamos configurar ou gerenciar servidores, em caso de picos de requisição a própria aws trata de escalar para atender as requisições.

- Para aumentar a performance do CodeBuild, uma boa prática é utilizar o cache em s3 de dependências utilizadas durante o build, para que não seja necessário baixá-las novamente.

- Caso seja necessário criptografar nossos artefatos automaticamente após a execução do CodeBuild, devemos associar uma chave KMS a ele.
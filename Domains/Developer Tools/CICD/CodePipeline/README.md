# AWS CodePipeline

<img height=100px; alt="code-deploy-logo" src="../../../../images/code-pipeline.png" />

<p>&nbsp;</p>

AWS CodePipeline is a **developer tool service** responsible **orchestrate end-to-end software release** based on a workflow that we define.

Através do CodePipeline é possível criar fluxos de *deployment*, integrando-se com os outros serviços da família de CI/CD disponibilizados pela AWS ou até mesmo serviços terceiros. Ou seja, podemos **criar nossas próprias pipelines** de implantação, sendo o serviço responsável por fazer CI/CD acontecer.

Um dos principais benefícios de se utilizar o CodePipeline é a automatização, pois através dele iremos configurar o CloudWatch para detectar alterações em nosso código, por exemplo a subida da uma nova versão em um bucket s3, que irá automaticamente '*triggar*' a nossa pipeline e realizar o deploy.

## Integrated Services

- AWS CI/CD services: CodeCommit, CodeBuild, CodeDeploy.
- AWS general services: Elastic Beanstalk, Cloudformation, Lambda, Elastic Container Service...
- Third-party services: Github, Jenkins...

## Tips

- Possui uma feature nativa para aprovações manuais.

- Duas formas de trigar nossas pipelines do CodePipeline automaticamente quando temos uma nova versão são:
    1. Usar o s3 como source e 'triggar' o CodePipeline sempre que um arquivo for atualizado ou adicionado.
    2. Usar o CodeCommit e 'triggar' o CodePipeline sempre que é realizado um git push ou git merge.


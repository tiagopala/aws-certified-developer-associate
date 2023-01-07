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
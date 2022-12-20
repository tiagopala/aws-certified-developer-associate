# AWS Step Functions

<img height=100px; alt="step_functions_logo" src="../../../images/step-functions.svg" />

<p>&nbsp;</p>

AWS Step functions is an **orchestration service for serverless applications**.

Por meio deste serviço é possível **criar**, **alterar** e **visualizar fluxos** utilizando uma **combinação de lambdas** como sendo uma série de steps.

Cada step é executado de acordo com a regra de negócio, sendo o output de uma lambda o input de outra lambda em sequência.

## Features

- **Sequencing** - Execução automática de cada step em ordem (*automatically trigger and track each step*)
- **Error Handling** - Tratativa de erros.
- **Retry Logic** - Permite o retry nativamente entre os steps caso aconteça inesperado.
- **Logging state of each step** (*debug and troubleshooting*) - Realiza o *logging* do estado em cada *step*, possibilitando a análise e facilitando a identificação e correção de possíveis problemas.

## Key Words

- **State Machine** - O próprio workflow
- **Task** - Cada step (lambda)

## Workflow Types

### Standard Workflow

- **Long-Running** - De longa duração, duráveis e auditáveis, podendo uma execução chegar até 1 ano. O histórico de execução fica disponível por 90 dias.
- **At-Most-Once Model** - Tasks não são executadas mais que uma vez, ao menos que seja configurado com ações de retry.
- **Non-Idempotent Actions** - Não idempotente significa que toda vez for solicitado, ele irá causar a alteração no estado. Exemplo: Envio de um e-mail, ele sempre irá gerar o envio de um novo e-mail.

### Express Workflow

- **Short-lived** - De curta duração, alto volume e geralmente para processamento de eventos.
- **At-Least-One** - Tem a possibilidade de ser executado mais de uma vez ou até em concorrência.
- **Idempotent Actions** - Ações que não causam alteração no estado, ou seja, caso requisições adicionais sejam realizadas o resultado sempre será o mesmo.

> Para facilitar, idempotente significa que requisições idênticas, caso sejam chamadas uma ou várias vezes, sempre terão o mesmo resultado. Caso isto não ocorra, é uma ação não idempotente.

**Express Workflows Types**

- **Synchronous Express Workflow** - Aguarda um retorno para execução do próximo step.
- **Asynchronous Express Workflow** - Não aguarda o retorno de uma ação para iniciar a outra.

## Workflow Patterns

<details>
    <summary>Sequential Workflow</summary>
    <img width=400px; alt="step-functions-sequential-workflow" src="../../../images/step-functions-sequential-workflow.png" />
</details>

<details>
    <summary>Parallel Workflow</summary>
    <img width=400px; alt="step-functions-parallel-workflow" src="../../../images/step-functions-parallel-workflow.png" />
</details>

<details>
    <summary>Branching Workflow</summary>
    <img width=400px; alt="step-functions-branching-workflow" src="../../../images/step-functions-branching-workflow.png" />
</details>
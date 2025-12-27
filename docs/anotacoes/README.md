# README.md anotado

## Visão geral
Este arquivo apresenta o contexto do repositório e explica, em alto nível, os módulos (lambdas, ecs e files). Ele orienta o leitor sobre tecnologias e escopo. Como prática de documentação, ele descreve o *porquê* e o *o quê* do projeto, servindo como porta de entrada para a arquitetura.

### Boas práticas destacadas
- **README como contrato**: explicita tecnologias e módulos, facilitando onboarding.
- **Separação por domínio**: organiza os exemplos por tipo de serviço (Lambdas, ECS).

## Trechos com anotações
1. **Título e descrição do projeto**: ajuda a identificar o repositório e seu contexto acadêmico.
2. **Tecnologias e frameworks**: lista o stack, útil para compreender requisitos de build/runtime.
3. **Distribuição dos códigos**: aponta os diretórios centrais, refletindo a arquitetura em módulos.
4. **Observações**: comunica limitações e instruções importantes para uso correto.

## Código completo
```markdown
# MBA-cloud-computing-serverless

Este é um repositório para agrupar codigos do MBA em Cloud Computing Serverless da [FullCycle](https://fullcycle.com.br).

## Tecnologias

### Foram usadas as seguintes tecnologias no projeto.
* Java 17
* Python
* Docker
* maven

### Frameworks de desenvolvimento.
* Spring Boot 3.2.5
* Quarkus 3.10.0


## Distribuição dos codigos
* lambdas 
  * pasta contendo os codigos usados nas aulas praticas 9,10,11,15,16,17,18,19,20.
* ecs
  * pasta contendo o codigo usado para ecr/ecs nas aulas praticas 12,13.
* files
  * pasta contendo arquivos usados para armazenamento no S3, para fim de replicar com maior exatidão o que foi implementado.


## Observaçoes
* Os códigos utilizados são de simples demonstração, não havendo extensivas regras, patterns, ou outras praticas de desenvolvimento.
* Para o bom funcionamento, observe se existem comentários solicitrando alguma substituição, e proceda conforme o solicitado.
```

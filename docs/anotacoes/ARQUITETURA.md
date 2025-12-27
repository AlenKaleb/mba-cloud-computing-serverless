# Visão de arquitetura (anotações)

## Panorama geral
O repositório está organizado em três áreas principais:
- **`lambdas/`**: funções serverless para exercícios (API Gateway, DynamoDB, SQS, EC2, SSM, Secrets Manager).
- **`ecs/`**: aplicação Spring Boot containerizada para execução em ECS/ECR.
- **`files/`**: objetos de exemplo para testes de armazenamento em S3.

## Conceitos arquiteturais relevantes
- **Serverless**: funções Lambda com integrações gerenciadas (API Gateway, DynamoDB, SQS).
- **Arquitetura orientada a eventos**: mensagens enviadas ao SQS para processamento assíncrono.
- **Configuração externa**: uso de `application.properties` e Parameter Store/Secrets Manager para evitar hardcode.
- **Containerização**: aplicação Java empacotada em container Docker para ECS.

## Padrões e boas práticas presentes
- **Separação por responsabilidade**: cada Lambda foca em um caso de uso específico.
- **Observabilidade básica**: logging do evento e de respostas críticas.
- **Uso de SDK oficial**: `boto3` e AWS SDK (via BOM) para consistência.
- **Empacotamento reprodutível**: Maven Wrapper fixando versão do build.

## Oportunidades de evolução (contexto didático)
- **Validação de entrada**: adicionar validação/contratos explícitos para payloads.
- **Tratamento de erros padronizado**: respostas consistentes em todas as Lambdas.
- **Segurança**: mover segredos e URLs de filas para variáveis de ambiente.

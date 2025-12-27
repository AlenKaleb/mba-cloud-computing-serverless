# lambdas/function-aula-20.py anotado

## Visão geral
Lambda que lê um segredo do AWS Secrets Manager e registra o valor. Demonstra integração com gerenciamento de segredos.

### Conceitos e padrões
- **Secrets Manager**: armazenamento seguro de segredos.
- **Cliente reutilizável**: inicializado fora do handler.
- **Logging**: usa `logging` para melhor observabilidade.

## Trechos com anotações
1. **Logger**: configuração global e nível de log.
2. **Client do Secrets Manager**: criação do `boto3.client('secretsmanager')`.
3. **Get secret**: `get_secret_value` obtém o valor.
4. **Tratamento de erros**: captura caso o segredo não exista.

## Código completo
```python
import boto3
import logging
import json

# Configurar o logger
logger = logging.getLogger()
logger.setLevel(logging.INFO)

# Criar um cliente para o Secrets Manager
secrets_client = boto3.client('secretsmanager')


def lambda_handler(event, context):
    # ID ou nome do segredo que você quer acessar
    secret_name = 'dev/my/secret'

    try:
        # Obter o valor do segredo
        response = secrets_client.get_secret_value(
            SecretId=secret_name
        )

        secret_value = response['SecretString']

        # Logar o valor do segredo
        logger.info(f"Secret Value: {secret_value}")

    except secrets_client.exceptions.ResourceNotFoundException:
        logger.error(f"Secret {secret_name} not found.")
    except Exception as e:
        logger.error(f"Error getting secret {secret_name}: {e}")

    return {
        'statusCode': 200,
        'body': 'Secret logged successfully'
    }
```

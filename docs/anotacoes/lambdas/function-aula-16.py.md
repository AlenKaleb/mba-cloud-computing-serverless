# lambdas/function-aula-16.py anotado

## Visão geral
Lambda que expõe operações CRUD em uma tabela DynamoDB (`customer`) via API Gateway proxy. Implementa GET (lista/por id), POST, PUT e DELETE.

### Conceitos e padrões
- **Roteamento por método + recurso**: simula controller.
- **DynamoDB**: usa operações `scan`, `query`, `put_item`, `delete_item`.
- **UUID**: gera identificadores únicos para novos registros.
- **Status HTTP sem framework**: status codes definidos manualmente.

### Boas práticas observadas
- **Logs do evento**: facilita troubleshooting.
- **Uso de `statusCode`**: respostas compatíveis com API Gateway.

## Trechos com anotações
1. **Criação do client DynamoDB**: `boto3.client('dynamodb')`.
2. **Parse do body**: JSON do API Gateway convertido em dict.
3. **GET /customer**: `scan` para leitura total (pode ser caro em produção).
4. **GET /customer/{id}**: `query` com chave primária.
5. **POST /customer**: cria item e retorna o registro criado.
6. **PUT /customer/{id}**: sobrescreve item com o id informado.
7. **DELETE /customer/{id}**: remove o item e retorna mensagem.

## Código completo
```python
import json
from uuid import uuid4

import boto3
from boto3.dynamodb.conditions import Key

print('Loading function')
def lambda_handler(event, context):
    global body
    statusCode = 200
    responseBody = ""

    if 'httpMethod' in event and 'resource' in event:
        rota = str(event['httpMethod']) + ' '+ str(event['resource'])
    else:
        responseBody = "Esta funçao devera serchamada via proxy do APi Gateway"
        statusCode = 400
        return {
            'statusCode': statusCode,
            'body': responseBody
        }

    print(json.dumps(event))

    tableName = 'customer'
    dynamodb = boto3.client('dynamodb')
    
    if event['body'] is not None:
        body = json.loads(event['body'])

    if rota == "GET /customer":
        response = dynamodb.scan(
            TableName=tableName
        )
        print(json.dumps(response))
        responseBody = response["Items"]
    elif rota == "GET /customer/{id}":
        id = event['pathParameters']['id']
        response = dynamodb.query(
            TableName=tableName,
            KeyConditionExpression="id=:id",
            ExpressionAttributeValues={
                ":id": {
                    "S": id
                }
            }
        )
        responseBody = response["Items"]
    elif rota == "POST /customer":
        uuid = str(uuid4())
        dynamodb.put_item(
            TableName=tableName,
            Item={
                'id': {'S': uuid},
                'name': {'S': body['name']}
            }
        )

        response = dynamodb.query(
            TableName=tableName,
            KeyConditionExpression="id=:id",
            ExpressionAttributeValues={
                ":id": {
                    "S": uuid
                }
            }
        )
        responseBody = response["Items"]
        statusCode = 201
    elif rota == "PUT /customer/{id}":
        id = event['pathParameters']['id']
        dynamodb.put_item(
            TableName=tableName,
            Item={
                'id': {'S': id},
                'name': {'S': body['name']}
            }
        )
        response = dynamodb.query(
            TableName=tableName,
            KeyConditionExpression="id=:id",
            ExpressionAttributeValues={
                ":id": {
                    "S": id
                }
            }
        )
        responseBody = response["Items"]
        statusCode = 202
    elif rota == "DELETE /customer/{id}":
        id = event['pathParameters']['id']
        dynamodb.delete_item(
            TableName=tableName,
            Item={
                'id': {'S': id}
            }
        )
        responseBody = "Deletado com sucesso"
    else:
        responseBody = "Rota nao implementada"
        statusCode = 500
        return {
            'statusCode': statusCode,
            'body': responseBody
        }
    return {
        'statusCode': statusCode,
        'body': json.dumps(responseBody)
    }
```

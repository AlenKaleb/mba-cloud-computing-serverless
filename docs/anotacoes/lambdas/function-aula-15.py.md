# lambdas/function-aula-15.py anotado

## Visão geral
Função Lambda acionada via API Gateway (proxy). Ela verifica método e recurso, lê o parâmetro `name` e responde de acordo com a rota.

### Conceitos e boas práticas
- **API Gateway Proxy**: uso de `httpMethod` e `resource` para roteamento.
- **Validação básica de entrada**: responde 400 quando não é chamada via proxy.
- **Logging**: registra o evento para depuração.

## Trechos com anotações
1. **Imports e log de inicialização**: `print('Loading function')` ajuda a notar cold starts.
2. **Validação do evento**: confere se a chamada veio do API Gateway proxy.
3. **Roteamento manual**: combina método + resource para selecionar a ação.
4. **Resposta**: retorna status HTTP e corpo serializado.

## Código completo
```python
import json

print('Loading function')
def lambda_handler(event, context):
    body = ""
    statusCode = 200

    if 'httpMethod' in event and 'resource' in event:
        rota = str(event['httpMethod']) + ' '+ str(event['resource'])
    else:
        body = "Esta funçao devera serchamada via proxy do APi Gateway"
        statusCode = 400
        return {
            'statusCode': statusCode,
            'body': body
        }

    print(json.dumps(event))

    name = event['queryStringParameters']['name']

    if rota == "GET /customer":
        body = "Ola "+name
    else:
        body = "Rota nao implementada"
        statusCode = 500
        return {
            'statusCode': statusCode,
            'body': body
        }
    return {
        'statusCode': statusCode,
        'body': json.dumps(body)
    }
```

# lambdas/function-aula-17.py anotado

## Visão geral
Lambda simples que envia o evento recebido para uma fila SQS. Útil para desacoplar processamento assíncrono.

### Conceitos e padrões
- **Event forwarding**: repassa eventos para fila.
- **Desacoplamento**: evita processamento síncrono no endpoint.
- **SQS client**: usa `boto3.client('sqs')`.

### Boas práticas
- **Logging do MessageId**: permite rastreabilidade.

## Trechos com anotações
1. **Serialização do evento**: `json.dumps(event)` para formar o corpo da mensagem.
2. **send_message**: envia para `QueueUrl` (deveria ser URL completa em produção).
3. **Log do MessageId**: confirma envio.

## Código completo
```python
import json

import boto3

print('Loading function')
def lambda_handler(event, context):
    message = json.dumps(event)

    sqs = boto3.client('sqs')
    resp = sqs.send_message(
        QueueUrl="teste-sqs",
        MessageBody=(
          message
        )
    )
    print(resp['MessageId'])
```

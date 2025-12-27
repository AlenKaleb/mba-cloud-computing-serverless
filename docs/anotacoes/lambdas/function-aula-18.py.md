# lambdas/function-aula-18.py anotado

## Visão geral
Lambda que inicia ou para instâncias EC2 com base em um parâmetro de ação. Mostra automação simples de infraestrutura.

### Conceitos e boas práticas
- **Infra como código**: operação programática sobre EC2.
- **Controle por evento**: `event['action']` determina start/stop.
- **Região explícita**: `region_name` fixa a região de operação.

### Observação
- O array `instances` contém placeholder e deve ser substituído por IDs reais.

## Trechos com anotações
1. **Client EC2**: estabelece conexão com AWS EC2.
2. **Lista de instâncias**: define alvo da operação.
3. **Ação**: `start` ou `stop` conforme evento.

## Código completo
```python
import boto3

print('Loading function')
def lambda_handler(event, context):
    ec2 = boto3.client('ec2', region_name='us-east-1')
    #colocar o id da instancia a ser parada ou uniciada
    instances = ['i-sua-instancia']

    if event['action'] == 'start':
        ec2.start_instances(InstanceIds=instances)
        print('instacias iniciadas: ' + str(instances))
    elif event['action'] == 'stop':
        ec2.stop_instances(InstanceIds=instances)
        print('instancias paradas: ' + str(instances))
    else:
        print('acao nao programada')
```

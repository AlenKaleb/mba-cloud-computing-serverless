# ecs/aulas-12-13/src/main/resources/application.properties anotado

## Visão geral
Define o nome da aplicação Spring Boot. Esse valor é usado por logs, métricas e, dependendo das integrações, identificação em observabilidade.

### Boas práticas
- **Configuração externa**: propriedades ficam separadas do código.
- **Nome consistente**: facilita rastreabilidade em ambientes distribuídos.

## Trechos com anotações
1. `spring.application.name`: identifica a aplicação no contexto do Spring Boot.

## Código completo
```properties
spring.application.name=java-ecs-spring
```

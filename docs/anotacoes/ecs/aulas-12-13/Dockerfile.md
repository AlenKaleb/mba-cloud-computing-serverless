# ecs/aulas-12-13/Dockerfile anotado

## Visão geral
Este Dockerfile empacota a aplicação Spring Boot em um container Java 17. A arquitetura segue o padrão **single jar**: o build gera um `.jar` executável e a imagem apenas o executa.

### Conceitos e boas práticas
- **Imagem base oficial**: `openjdk:17` garante runtime compatível com Java 17.
- **Build separado de runtime**: pressupõe que o jar já foi gerado pelo Maven no estágio anterior.
- **Exposição de porta**: `EXPOSE 8080` documenta a porta do serviço.
- **Entrypoint explícito**: evita shell para reduzir ambiguidades.

## Trechos com anotações
1. **Base image**: define o ambiente de execução com JDK.
2. **ADD do jar**: copia o artefato final para dentro da imagem.
3. **EXPOSE**: indica a porta padrão do Spring Boot.
4. **ENTRYPOINT**: inicia o processo principal.

## Código completo
```dockerfile
FROM openjdk:17
ADD target/java-ecs-spring-0.0.1-SNAPSHOT.jar java-ecs.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","java-ecs.jar"]
```

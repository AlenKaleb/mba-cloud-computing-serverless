# ecs/aulas-12-13/src/main/java/org/acme/javaecsspring/JavaEcsSpringApplication.java anotado

## Visão geral
Classe de entrada da aplicação Spring Boot. Ela habilita o auto-configuration e inicia o servidor web embutido (Tomcat por padrão).

### Conceitos e padrões
- **Bootstrapping**: `SpringApplication.run` inicializa o contexto e servidores.
- **Anotação composta**: `@SpringBootApplication` agrega `@Configuration`, `@EnableAutoConfiguration` e `@ComponentScan`.

## Trechos com anotações
1. `@SpringBootApplication`: habilita autoconfiguração e busca de componentes.
2. `main`: ponto de entrada Java padrão; inicia o contexto Spring.

## Código completo
```java
package org.acme.javaecsspring;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class JavaEcsSpringApplication {

	public static void main(String[] args) {
		SpringApplication.run(JavaEcsSpringApplication.class, args);
	}

}
```

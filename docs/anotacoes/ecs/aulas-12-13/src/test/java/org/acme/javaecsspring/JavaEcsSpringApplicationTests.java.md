# ecs/aulas-12-13/src/test/java/org/acme/javaecsspring/JavaEcsSpringApplicationTests.java anotado

## Visão geral
Teste de smoke do contexto Spring Boot. Verifica se o aplicativo consegue inicializar sem falhas.

### Conceitos
- **Testes de contexto**: validam wiring/beans do Spring.
- **JUnit 5**: framework de testes padrão.

## Trechos com anotações
1. `@SpringBootTest`: sobe o contexto completo da aplicação.
2. `contextLoads`: teste vazio que falha caso o contexto não inicialize.

## Código completo
```java
package org.acme.javaecsspring;

import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
class JavaEcsSpringApplicationTests {

	@Test
	void contextLoads() {
	}

}
```

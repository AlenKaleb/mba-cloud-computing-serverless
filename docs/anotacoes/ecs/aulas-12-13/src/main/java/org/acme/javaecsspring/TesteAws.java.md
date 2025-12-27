# ecs/aulas-12-13/src/main/java/org/acme/javaecsspring/TesteAws.java anotado

## Visão geral
Controller REST simples com endpoint `GET /teste-aws`. Demonstra o padrão MVC do Spring, com mapeamento de rota e parâmetros de query.

### Conceitos e boas práticas
- **Controller dedicado**: separa a camada de apresentação.
- **HTTP semantics**: `@ResponseStatus` explicita o status de resposta.
- **RequestParam**: validação mínima de entrada (parâmetro obrigatório).

## Trechos com anotações
1. `@RestController`: combina `@Controller` + `@ResponseBody` para retornar JSON/texto.
2. `@RequestMapping("teste-aws")`: prefixa o caminho do recurso.
3. `@GetMapping`: define o verbo HTTP GET.
4. `@RequestParam("nome")`: captura query string e insere no retorno.

## Código completo
```java
package org.acme.javaecsspring;

import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("teste-aws")
public class TesteAws {

    @GetMapping
    @ResponseBody
    @ResponseStatus(HttpStatus.OK)
    public String get(@RequestParam("nome") String name) {
        return "Bem vindo ".concat(name).concat("!");
    }
}
```

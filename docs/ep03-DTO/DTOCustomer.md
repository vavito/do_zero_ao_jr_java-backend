# DO ZERO AO JR: JAVA BACKEND — Episódio 3

Uma das coisas que mais comecei a entender no backend é que nem tudo que funciona está, de fato, bem estruturado.

Enquanto desenvolvia algumas rotas da aplicação, aprendi melhor o papel dos DTOs e por que separar `Request` e `Response` faz tanta diferença.

## Request e Response na prática

Pense assim:

- O `Request` é o que a aplicação recebe.
- O `Response` é o que ela devolve.

Parece simples — e é.

Mas essa separação evita um erro muito comum: expor diretamente a entidade da aplicação.

Sem DTOs, a API pode acabar:
- expondo dados desnecessários,
- ficando muito acoplada ao banco,
- e mais difícil de manter no futuro.

Com DTOs, a aplicação ganha uma “camada de organização” entre o cliente e a regra de negócio.

## E por que usar `record`?

Porque DTO serve apenas para transportar dados.

Na maioria das vezes, não precisamos alterar esses dados depois que eles chegam ou saem da aplicação.

O `record` resolve isso muito bem:

- cria objetos imutáveis,
- reduz código repetitivo,
- e deixa tudo mais limpo.

## Exemplo

```java
public record CustomerRequestDTO(
    String name,
    String email
) {}
```

O mais interessante é perceber como pequenas decisões de arquitetura deixam o projeto mais organizado e escalável no longo prazo.
# Duas formas de injetar dependência e como NÃO injetar dependência no Spring Boot em 2026

## 1ª Forma Correta - `@Autowired`

A anotação `@Autowired` em atributos injeta automaticamente essas dependências na classe.

### VANTAGEM:
- menos código
- mais explícito na intenção

---

## 2ª Forma Correta (e mais recomendada) - `@RequiredArgsConstructor`

A anotação `@RequiredArgsConstructor` vem do Lombok e gera automaticamente um construtor contendo todos os atributos `final` (e também os marcados com `@NonNull`).

### VANTAGEM:
- menos código AINDA
- mais bonito (na minha opinião)

---

# Comparação

## COM `@Autowired`

```java
@Service
public class PedidoService {

    @Autowired
    private PedidoRepository pedidoRepository;

    @Autowired
    private ClienteService clienteService;

    @Autowired
    private PagamentoService pagamentoService;
}
```

---

## COM `@RequiredArgsConstructor`

```java
@Service
@RequiredArgsConstructor
public class PedidoService {

    private final PedidoRepository pedidoRepository;
    private final ClienteService clienteService;
    private final PagamentoService pagamentoService;
}
```

---

# E, afinal, então como NÃO injetar dependência?

De forma manual, é lógico.

Frameworks como Spring Boot vêm exatamente com essa vantagem: reduzir código boilerplate.

Pegando o código acima, ficaria:

```java
@Service
public class PedidoService {

    private final PedidoRepository pedidoRepository;
    private final ClienteService clienteService;
    private final PagamentoService pagamentoService;

    // Construtor manual
    public PedidoService(PedidoRepository pedidoRepository,
                         ClienteService clienteService,
                         PagamentoService pagamentoService) {
        this.pedidoRepository = pedidoRepository;
        this.clienteService = clienteService;
        this.pagamentoService = pagamentoService;
    }

    // Aqui você pode adicionar métodos que usam as dependências
}
```
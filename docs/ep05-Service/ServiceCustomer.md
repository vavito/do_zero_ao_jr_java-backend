# DO ZERO AO JR: JAVA BACKEND — Episódio 5 - Service

Neste episódio, vamos explorar melhor o papel da camada `Service` dentro de uma aplicação organizada em DDD Light.

O `Service` existe justamente para centralizar as regras e operações da aplicação.

É nele que normalmente ficam:

- validações;
- regras de negócio;
- fluxo da aplicação;
- e comunicação com o banco através do `Repository`.

## Injetando o Repository

Para que o `Service` consiga salvar, buscar ou deletar dados no banco, precisamos acessar o `CustomerRepository`.

Aprendi que existem duas formas comuns de fazer isso.

## Manualmente

```java
@Service
public class CustomerService {

    private final CustomerRepository repository;

    public CustomerService(CustomerRepository repository) {
        this.repository = repository;
    }

    public Customer createCustomer(Customer customer) {
        return repository.save(customer);
    }
}
```

## Automaticamente com Lombok

```java
@Service
@RequiredArgsConstructor
public class CustomerService {

    private final CustomerRepository repository;

    public Customer createCustomer(Customer customer) {
        return repository.save(customer);
    }
}
```

## Por que o segundo caso funciona?

Porque o Lombok gera automaticamente o construtor para os atributos `final`.

A anotação `@RequiredArgsConstructor` cria automaticamente um construtor contendo todos os campos `final` e também os campos marcados com `@NonNull`.

Isso reduz bastante código repetitivo e deixa a classe mais limpa e legível.

## O principal aprendizado

Com o tempo, comecei a perceber que o `Service` ajuda a:

- centralizar regras da aplicação;
- separar responsabilidades entre camadas;
- evitar lógica de negócio no `Controller`;
- e manter a aplicação mais organizada conforme cresce.
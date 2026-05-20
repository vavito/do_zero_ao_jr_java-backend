# DO ZERO AO JR: JAVA BACKEND — Episódio 6 - Controller

Neste episódio, vamos entender melhor o papel do `Controller` dentro de uma API REST.

O `Controller` funciona como a porta de entrada da aplicação. É ele quem:

- recebe requisições HTTP;
- chama o `Service`;
- e devolve uma resposta para o cliente.

Ou seja, o `Controller` não deveria conter regra de negócio. Seu foco deve ser apenas controlar o fluxo da requisição e da resposta.

---

# ResponseEntity

Uma das coisas mais importantes que aprendi foi o uso de `ResponseEntity`.

Em nossos métodos, como o `GetMapping`, é possível retornar apenas um DTO para o usuário:

```java
@GetMapping("/{id}")
public CustomerResponseDTO find(@PathVariable Long id) {
    return service.find(id);
}
```

Isso funciona. O Spring já retorna `200 OK`.

Mas usando `ResponseEntity`, ganhamos controle total sobre a resposta HTTP:

```java
@GetMapping("/{id}")
public ResponseEntity<CustomerResponseDTO> find(@PathVariable Long id) {
    return ResponseEntity.ok(service.find(id));
}
```

Com isso conseguimos controlar:

- status HTTP;
- body;
- headers;
- respostas sem conteúdo;
- e respostas personalizadas.

---

# Principais retornos HTTP

## 1. 200 OK

Com `ResponseEntity`:

```java
return ResponseEntity.ok(response);
```

Usado normalmente em:

- GET
- PUT
- PATCH

### O que significa?

> A requisição deu certo.

---

## 2. 201 Created

Com `ResponseEntity`:

```java
return ResponseEntity.status(HttpStatus.CREATED).body(response);
```

Usado normalmente em:

- POST

### O que significa?

> A requisição deu certo e um novo recurso foi criado.

---

## 3. 204 No Content

Com `ResponseEntity`:

```java
return ResponseEntity.noContent().build();
```

Usado normalmente em:

- DELETE

### O que significa?

> A operação deu certo, mas não existe conteúdo para retornar.

Por isso normalmente usamos:

```java
ResponseEntity<Void>
```

O `Void` indica que a resposta não terá body.
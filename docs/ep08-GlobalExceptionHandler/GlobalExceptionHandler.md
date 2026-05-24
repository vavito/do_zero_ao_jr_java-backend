# DO ZERO AO JR: JAVA BACKEND — Global Exception Handler

Uma das coisas mais importantes em uma API não é apenas tratar o sucesso das requisições, mas também tratar os erros da forma correta.

É aí que entra o `Global Exception Handler`.

A ideia dele é simples:

- capturar exceções da aplicação;
- transformar isso em respostas HTTP padronizadas;
- e evitar que o cliente receba erros técnicos gigantescos.

---

# Sem tratamento global

Sem um tratamento global, a API pode acabar devolvendo algo assim:

```txt
org.springframework.web.multipart.MultipartException:
Failed to parse multipart servlet request
	at org.springframework.web.multipart...
	at org.springframework.web.servlet...
	at jakarta.servlet.http...
```

Além de feio, isso expõe detalhes internos da aplicação e dificulta o entendimento de quem está consumindo a API.

---

# Com Global Exception Handler

Com um `GlobalExceptionHandler`, conseguimos devolver respostas muito mais limpas:

```json
{
  "status": 400,
  "error": "Bad Request",
  "message": "Formato de arquivo não suportado. Envie apenas MP3 ou WAV."
}
```

---

# Como isso funciona?

A anotação:

```java
@RestControllerAdvice
```

faz essa classe “observar” todos os controllers da aplicação.

Então, quando alguma exceção é lançada no `Controller`, `Service` ou `Domain`, o Spring procura métodos marcados com:

```java
@ExceptionHandler(DomainException.class)
```

Isso significa:

> “Quando acontecer uma `DomainException`, use este método para montar a resposta HTTP.”

O `Rest` em `@RestControllerAdvice` também indica que a resposta será enviada diretamente no body da requisição, normalmente em JSON.

---

# O principal aprendizado

O `Global Exception Handler` ajuda a deixar a API:

- mais profissional;
- mais segura;
- mais padronizada;
- e muito mais amigável para quem consome os endpoints.

Em APIs REST, tratar erros corretamente é tão importante quanto tratar os casos de sucesso.
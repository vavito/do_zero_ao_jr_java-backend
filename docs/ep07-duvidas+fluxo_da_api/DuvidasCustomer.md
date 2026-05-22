# DO ZERO AO JR: JAVA BACKEND — DTOs, Entities e Fluxo da API

Quando começamos a trabalhar com APIs REST, uma dúvida muito comum é:

> por que não retornar a Entity diretamente no Controller?

Vamos imaginar uma entidade `Customer`:

```java
public class Customer {
    private Long id;
    private String name;
    private String email;
    private String cpf;
    private String phone;
    private String password;
}
```

O problema é que a Entity representa a tabela do banco de dados.

Ou seja, ela pode conter informações sensíveis que não deveriam ser expostas na API, como CPF e senha.

Por isso usamos DTOs de resposta:

```java
public record CustomerResponseDTO(
        Long id,
        String name,
        String email,
        String phone
) {
}
```

Com isso, conseguimos controlar exatamente quais dados serão enviados para quem consumir a API.

---

# O Service trabalha com Entity

Dentro do `Service`, normalmente trabalhamos com a entidade real do sistema.

Por isso métodos auxiliares (dentro de Service) como:

```java
private Customer findById(Long id)
```

retornam `Customer` e não `CustomerResponseDTO`.

Isso acontece porque o Service precisa:

- atualizar dados;
- salvar alterações;
- aplicar regras de negócio;
- e manipular a entidade completa.

O DTO existe apenas para comunicação externa da API.

---

# Fluxo correto da API

Na prática, o fluxo costuma funcionar assim:

1. Controller recebe `RequestDTO`
2. Service transforma DTO em Entity
3. Repository salva/busca no banco
4. Service transforma Entity em `ResponseDTO`
5. Controller retorna o DTO para o cliente

## Exemplo

Cliente envia:

```json
{
  "name": "João",
  "email": "joao@email.com",
  "cpf": "12345678909",
  "phone": "(11) 99999-9999",
  "password": "12345678"
}
```

O `Controller` recebe isso como `CustomerRequestDTO`.

O `Service` transforma em `Customer`.

O `Repository` salva no banco.

Depois, o `Service` transforma a entidade salva em `CustomerResponseDTO`.

Resposta da API:

```json
{
  "id": 1,
  "name": "João",
  "email": "joao@email.com",
  "phone": "(11) 99999-9999"
}
```

Perceba que CPF e senha não aparecem na resposta.

---

# O principal aprendizado

Separar Entity e DTO não é apenas “mais organização”.

Isso ajuda a:

- proteger dados sensíveis;
- separar responsabilidades;
- reduzir acoplamento;
- e manter a API mais segura e sustentável conforme cresce.
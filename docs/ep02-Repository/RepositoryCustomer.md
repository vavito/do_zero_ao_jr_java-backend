# DO ZERO AO JR: JAVA BACKEND — Episódio 2 - Repository 🚀

Dando continuidade à documentação do meu aprendizado com Spring Boot, hoje o foco foi a camada de persistência: a criação do `CustomerRepository`.

Diferente de abordagens tradicionais onde você precisa escrever manualmente as consultas SQL para operações básicas, o Spring Data JPA simplifica tudo através de interfaces.

## 📌 O que aprendi na Task A5 (Customer Repository)

A declaração é simples, mas o conceito por trás é fundamental:

```java
public interface CustomerRepository extends JpaRepository<Customer, Long> {}
```

## 🤔 Por que essa estrutura é necessária?

O segredo está no **Generics** do `JpaRepository`, que exige dois parâmetros essenciais:

1. **A Entidade (`Customer`)**  
   Para o Spring saber qual tabela ele deve gerenciar.

2. **O Tipo do ID (`Long`)**  
   Para tipar corretamente os métodos de busca e garantir a segurança dos dados.

## ✅ Resultado

Com uma única linha de código, ganhei acesso a todos os métodos de CRUD (**Salvar, Listar e Deletar**), mantendo o código limpo e seguindo as melhores práticas de desenvolvimento.
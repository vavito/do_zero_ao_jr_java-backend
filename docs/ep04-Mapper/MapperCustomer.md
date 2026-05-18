# DO ZERO AO JR: JAVA BACKEND — Episódio 4 - Mapper

Neste episódio, o aprendizado foi sobre uma peça simples, mas muito importante na organização do backend: o `Mapper`.

Quando comecei a separar melhor `Entity`, `RequestDTO` e `ResponseDTO`, surgiu uma dúvida natural:

> quem fica responsável por transformar uma coisa na outra?

É aí que entra o `Mapper`.

Na prática, ele funciona como uma “ponte” entre os dados que entram, os dados que saem e a entidade principal da aplicação.

No meu caso, criei um `CustomerMapper` com três responsabilidades principais:

- transformar uma entidade `Customer` em `CustomerResponseDTO`;
- transformar um `CustomerRequestDTO` em uma entidade `Customer`;
- atualizar uma entidade existente com os dados recebidos no DTO.

Isso ajuda a evitar que essa lógica de conversão fique espalhada pelo `Controller` ou pelo `Service`, os quais já possuem suas próprias responsabilidades e não deveriam lidar com essa lógica.

E esse ponto fez bastante sentido para mim:

- o `Controller` deve lidar com a entrada e saída da requisição;
- o `Service` deve cuidar da regra de aplicação;
- e o `Mapper` deve cuidar da conversão entre objetos.

## Mantendo a entidade responsável pelas próprias regras

Outro detalhe importante foi manter a entidade no controle das próprias alterações.

Em vez de alterar os atributos diretamente, utilizei métodos como:

```java
customer.changeName(dto.name());
customer.changeEmail(dto.email());
customer.changePhoneNumber(dto.phone());
```

Assim, a entidade continua protegendo suas regras internas, enquanto o `Mapper` apenas direciona os dados para os métodos corretos.

Também adicionei verificações contra `null`, evitando erros simples quando algum objeto não existir.

## O principal aprendizado

No fim, entendi que o `Mapper` não está ali apenas para “copiar dados”.

Ele ajuda a:

- deixar o código mais organizado;
- reduzir acoplamento entre camadas;
- e tornar o projeto mais fácil de manter conforme a aplicação cresce.

Pequenas separações como essa fazem muita diferença na estrutura de um backend mais limpo.
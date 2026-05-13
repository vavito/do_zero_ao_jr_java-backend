# DO ZERO AO JR: JAVA BACKEND — Episódio 1 - Entity

Decidi iniciar esta série de documentação para registrar minha evolução no desenvolvimento backend com Java e Spring Boot, compartilhando aprendizados adquiridos durante a construção de uma aplicação real.

Mais do que documentar tarefas específicas de um projeto, a proposta é transformar experiências práticas em conhecimento reutilizável — tanto para mim no futuro quanto para outras pessoas que também estão estudando backend e boas práticas de desenvolvimento.

Neste primeiro aprendizado, trabalhei na criação da entidade `Customer` dentro de uma estrutura baseada em DDD Light, utilizando camadas como `domain`, `service`, `controller`, `repository`, `dto` e `mapper`.

Durante essa implementação, alguns conceitos importantes ficaram ainda mais claros para mim:

* O uso da anotação `@Entity` para representar corretamente uma entidade persistida no banco de dados.
* O fato de que o Spring Data JPA/Hibernate já realiza automaticamente o mapeamento dos atributos da classe para colunas no banco, mesmo sem o uso explícito de `@Column`.
* O uso de `@Column` passa a fazer mais sentido quando precisamos definir regras específicas, como restrições de unicidade:

```java
@Column(unique = true)
```

Além da parte técnica, também revisei práticas importantes relacionadas ao fluxo de trabalho com Git:

* Criar branches separadas para cada feature ou task.
* Trabalhar e commitar diretamente na branch da funcionalidade.
* Utilizar Pull Requests como parte do processo de integração.
* Remover branches após o merge para manter o repositório mais organizado.

Tenho percebido cada vez mais que aprender desenvolvimento backend não envolve apenas fazer a funcionalidade funcionar, mas também entender padrões, organização de projeto e decisões que tornam o código mais sustentável no longo prazo.

Essa série será uma forma de acompanhar essa evolução de maneira mais estruturada e consciente. 🚀

#Java #SpringBoot #Backend #DDD #JPA #Hibernate #Git #CleanCode #DesenvolvimentoDeSoftware

# Clean Architecture no ReactJs

Link da Aula: [Aqui](https://www.youtube.com/watch?v=iUQVZHzqGuc)

## Camada Domain

A camada de Domain é o local onde ficará as regras de negócio. 
Essa camada é comumente composta de interfaces. **Não contem implementação.**

- Authentication

## Camada Data Layer

É a camada que contem as implementações dos casos de uso. 
A camada **Data Layer depende de Domain.**

Exemplos de nome:

- ApiAuthentication
- RemoteAuthentication

Esses exemplos são nomes possíveis para criar implementação da interface 
Authentication do Domain.

Aqui será feito:

- Tratamento da API
- Tratamento dos erros da API

Essa implementação porem não será responsável por acessa a API, essa que utilizará
de outra interface chamada por exemplo **HttpPostClient**.

## Camada de Infra

A camada de **Infra** é onde geralmente fica as implementações que utilizam 
**frameworks externos.** Aqui por exemplo, será encontrado o **AxiosHttpClient**
que fará a implementação de **HttpPostClient**, utilizando o framework **Axios.**

A camada **Infra depende do Data Layer.**

## Presentation

É a camada de apresentação de dados, normalmente criada separada da UI. 
Sua função é pegar um dado (por exemplo, que retornou da API) e converter 
para o formato que nossa tela precisa.

Normalmente é difícil de se separar a UI e Presentation quando utilizamos o React, por exemplo.

A camada **Presentation depende do Domain**, ou seja, alguem tem
que fazer a implementação para que a Presentation possa utilizar.

## Camada de Validation

É a camada responsável implementar as interfaces de validação presentes no **Presenter.**
A camada **Validation depende do Presenter.**

Exemplos:

- RequiredFieldValidation
- EmailFieldValidation

## Main Layer

A **Main Layer** será responsável por fornecer as implementações para as outras camadas,
dessa forma, apenas ela é dependente de tudo, para que as outras camadas sejam desacopladas.

O Design Pattern presente nessa camada é chamado **Composition Root**, é a "camada sacrificada".

Essa camada utiliza da Inversão e Injeção de Dependencias para se fazer funcionar.

Presente nessa Layer:

- Factories
- Adapters
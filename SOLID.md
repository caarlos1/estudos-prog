# Princípios do SOLID

## S - SRP - Single Responsability Principle (Princípio da Responsabilidade Única)

Uma entidade ou classe deve ter um, e apenas um montivo para ser alterada. 
Ou seja, ela deve fazer apenas uma coisa.

## O - OCP - Open/Closed Principle (Princípio do Aberto/Fechado)

Entidades de software devem ser abertas para extensão 
e fechadas para modificação.

É necessário pensar de forma que novas feauteres não necessitem
de modificações em suas classes e apenas adição de código.

Utilize a herança para compartilhar comportamentos e extenda as 
classes em vez de adiciona codicionais toda vez que for necessário 
adicionar uma função.

## L - LSP - Liskov Substitution Principle (Princípio da Substituição de Liskov)

Classes derivadas devem poder ser substituídas por suas classes bases.

Ou seja, ao instanciar uma classe derivada, deve ser possível tipala
como sua classe base. Ex:

```csharp
Cliente cliente = 
    new ClienteContratado("Carlos Roberto", DateTime.Today);

var premium = cliente.ClientePremium();
```

Esse princípio é importante para conseguirmos definir se uma classe
deve ou não ser derivada de outra. Nos ajudando a melhorar a modelagem
de nossas classes e saber quando deve haver uma extensão entre classes.

## I - Interface Segregation Principle (Princípio da Segregação de Interfaces)

Clientes não devem ser forçados a depender de métodos que não usam.

Sendo assim, quando necessário, deve-se segregar as interfaces.

```csharp
public interface IAve
{
    void Bicar();
    void Voar();
}
```

Um exemplo é um pinguim que não poderia ser obrigado a implementar a 
interface acima pois pinguins não voam.

Uma solução seria segregar a classe acima, dividindo em duas interfaces.

```csharp
public interface IAve
{
    void Bicar();
}

public interface IAveVoadora : IAve
{
    void Voar();
}
```

Dessa forma Pinguin pode usar a interface IAve, e as aves que voam
possuem a IAveVoadora.

## D - DIP - Dependency Inversion Principle (Princípio da Inversão de Dependência)

Dependa de uma abstração e não de uma implementação. Pois, implementações
geram muito mais dependencias que uma abastração.

```csharp
public interface ILeitorArquivo
{
    void Ler(string caminho);
}

public class LeitorTxt : ILeitorArquivo
{
    public void Ler(string caminho) 
    {
        //... Implementação
    }
}
```

### Abstração

```csharp
public class Test
{
    private readonly ILeitorArquivo _leitor;

    public Test(ILeitorArquivo leitor) =>
        _leitor = leitor;

    public void Ler(string caminho) =>
        _leitor.Ler(string caminho);
}
```
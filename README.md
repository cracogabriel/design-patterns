## Padrão de Projeto: Strategy

> **arquivo:** [src/strategy/main.ts](https://github.com/cracogabriel/design-patterns/blob/main/src/strategy/main.ts)

### O que é o Padrão de Projeto Strategy?

O Padrão de Projeto Strategy é um padrão de design comportamental que permite selecionar um algoritmo em tempo de execução a partir de uma família de algoritmos. Ele permite que o algoritmo varie independentemente dos clientes que o utilizam.

### Implementação

Neste código, o Padrão de Projeto Strategy é implementado por meio de uma classe `Context`, um conjunto de estratégias concretas e uma interface que define os métodos de estratégia.

#### Classe Context

A classe `Context` encapsula o objeto de estratégia e fornece métodos para definir a estratégia e executar o algoritmo.

```typescript
class Context {
  private strategy: Strategy;

  constructor(strategy: Strategy) {
    this.strategy = strategy;
  }

  public setStrategy(strategy: Strategy) {
    this.strategy = strategy;
  }

  public doSomeBusinessLogic(): void {
    const result = this.strategy.doAlgorithm(["a", "b", "c", "d", "e"]);
    console.log(result.join(","));
  }
}
```

#### Interface Strategy

A interface `Strategy` declara um método que todas as estratégias concretas devem implementar.

```typescript
interface Strategy {
  doAlgorithm(data: string[]): string[];
}
```

#### Estratégias Concretas

As classes de estratégia concretas (`ConcreteStrategyA` e `ConcreteStrategyB`) implementam o algoritmo definido na interface `Strategy`.

```typescript
class ConcreteStrategyA implements Strategy {
  public doAlgorithm(data: string[]): string[] {
    return data.sort();
  }
}

class ConcreteStrategyB implements Strategy {
  public doAlgorithm(data: string[]): string[] {
    return data.reverse();
  }
}
```

### Uso

Para usar o Padrão de Projeto Strategy:

1. Crie um objeto de contexto e inicialize-o com uma estratégia concreta.
2. Opcionalmente, altere a estratégia em tempo de execução usando o método `setStrategy`.
3. Chame o método `doSomeBusinessLogic` para executar o algoritmo.

Exemplo:

```typescript
const context = new Context(new ConcreteStrategyA());
context.doSomeBusinessLogic(); // Saída: a,b,c,d,e

context.setStrategy(new ConcreteStrategyB());
context.doSomeBusinessLogic(); // Saída: e,d,c,b,a
```

### Benefícios

- Permite a seleção de algoritmos em tempo de execução.
- Promove a separação de preocupações ao encapsular algoritmos em classes separadas.
- Facilita a adição de novos algoritmos sem modificar o código existente.

### Quando Usar

Use o Padrão de Projeto Strategy quando:

- Você tem vários algoritmos para realizar uma tarefa e deseja alternar entre eles dinamicamente.
- Você precisa isolar os detalhes de implementação de um algoritmo do código do cliente.
- Você tem uma classe com um comportamento que pode ser estendido ou alterado por várias subclasses.

### Diagrama UML

![Estrutura do padrão de projeto Strategy](https://refactoring.guru/images/patterns/diagrams/strategy/structure.png)

> **Material usado:** https://refactoring.guru/pt-br/design-patterns/strategy

## Padrão de Projeto: Factory Method

> **arquivo:** [src/factory/main.ts](https://github.com/cracogabriel/design-patterns/blob/main/src/factory/main.ts)

### O que é o Padrão de Projeto Factory Method?

O Padrão de Projeto Factory Method é um padrão de design criacional que fornece uma interface para criar objetos em uma superclasse, mas permite que as subclasses alterem o tipo de objetos que serão criados.

### Implementação

Neste código, o Padrão de Projeto Factory Method é implementado por meio de uma classe abstrata `Creator`, suas subclasses concretas (`ConcreteCreator1` e `ConcreteCreator2`), e interfaces e classes de produtos.

#### Classe Abstrata Creator

A classe `Creator` declara o método de fábrica abstrato que as subclasses devem implementar para criar produtos.

```typescript
abstract class Creator {
  public abstract factoryMethod(): Product;

  public someOperation(): string {
    const product = this.factoryMethod();
    return `Creator: The same creator's code has just worked with ${product.operation()}`;
  }
}
```

#### Subclasses Concretas Creator

As subclasses concretas (`ConcreteCreator1` e `ConcreteCreator2`) implementam o método de fábrica para criar instâncias específicas de produtos.

```typescript
class ConcreteCreator1 extends Creator {
  public factoryMethod(): Product {
    return new ConcreteProduct1();
  }
}

class ConcreteCreator2 extends Creator {
  public factoryMethod(): Product {
    return new ConcreteProduct2();
  }
}
```

#### Interface e Classes de Produto

A interface `Product` define o método que os produtos concretos devem implementar.

```typescript
interface Product {
  operation(): string;
}

class ConcreteProduct1 implements Product {
  public operation(): string {
    return "{Resultado do ConcreteProduct1}";
  }
}

class ConcreteProduct2 implements Product {
  public operation(): string {
    return "{Resultado do ConcreteProduct2}";
  }
}
```

#### Cliente

A função `clientCode` recebe uma instância de `Creator` e chama seus métodos, sem estar ciente da classe específica do criador ou do produto.

```typescript
function clientCode(creator: Creator) {
  console.log(
    "Client: I'm not aware of the creator's class, but it still works."
  );
  console.log(creator.someOperation());
}
```

### Uso

Para usar o Padrão de Projeto Factory Method:

1. Crie uma instância da classe de criador desejada.
2. Passe essa instância para o código do cliente.
3. O código do cliente chama o método `someOperation`, que utiliza o método de fábrica para criar um produto.

Exemplo:

```typescript
console.log("App: Launched with the ConcreteCreator1.");
clientCode(new ConcreteCreator1());
console.log("");

console.log("App: Launched with the ConcreteCreator2.");
clientCode(new ConcreteCreator2());
```

### Benefícios

- Permite a criação de objetos sem especificar explicitamente suas classes.
- Promove o princípio do encapsulamento, pois o código do cliente opera em interfaces, não em implementações concretas.
- Facilita a adição de novos tipos de produtos sem modificar o código existente.

### Quando Usar

Use o Padrão de Projeto Factory Method quando:

- O sistema precisa ser independente das classes de produtos que cria.
- O sistema deseja fornecer uma biblioteca de classes de produtos e deixar os usuários estender essas classes sem modificar o código existente.
- O sistema precisa permitir a configuração de um objeto com uma de várias variantes.

### Diagrama UML

![A estrutura do código após a aplicação do padrão Factory Method](https://refactoring.guru/images/patterns/diagrams/factory-method/structure.png)

> **Material usado:** https://refactoring.guru/pt-br/design-patterns/factory-method

## Padrão de Projeto: Facade

> **arquivo:** [src/facade/main.ts](https://github.com/cracogabriel/design-patterns/blob/main/src/facade/main.ts)

### O que é o Padrão de Projeto Facade?

O Padrão de Projeto Facade é um padrão de design estrutural que fornece uma interface unificada para um conjunto de interfaces em um subsistema. Ele define uma interface de nível mais alto que facilita o uso do subsistema, ocultando sua complexidade interna.

### Implementação

Neste código, o Padrão de Projeto Facade é implementado por meio de uma classe `Facade`, que simplifica a interação com os subsistemas `Subsystem1` e `Subsystem2`.

#### Classe Facade

A classe `Facade` fornece uma interface simplificada para interagir com os subsistemas. Ela inicializa os subsistemas e define métodos que coordenam suas operações.

```typescript
class Facade {
  protected subsystem1: Subsystem1;
  protected subsystem2: Subsystem2;

  constructor(subsystem1?: Subsystem1, subsystem2?: Subsystem2) {
    this.subsystem1 = subsystem1 || new Subsystem1();
    this.subsystem2 = subsystem2 || new Subsystem2();
  }

  public operation(): string {
    let result = "Facade initializes subsystems:\n";
    result += this.subsystem1.operation1();
    result += this.subsystem2.operation1();
    result += "Facade orders subsystems to perform the action:\n";
    result += this.subsystem1.operationN();
    result += this.subsystem2.operationZ();

    return result;
  }
}
```

#### Subsistemas

Os subsistemas (`Subsystem1` e `Subsystem2`) são classes que executam operações específicas.

```typescript
class Subsystem1 {
  public operation1(): string {
    return "Subsystem1: Pronto!\n";
  }

  public operationN(): string {
    return "Subsystem1: Vai!\n";
  }
}

class Subsystem2 {
  public operation1(): string {
    return "Subsystem2: Prepare-se!\n";
  }

  public operationZ(): string {
    return "Subsystem2: Fogo!";
  }
}
```

#### Cliente

A função `clientCode` recebe uma instância de `Facade` e interage com o sistema através dela.

```typescript
function clientCode(facade: Facade) {
  console.log(facade.operation());
}
```

### Uso

Para usar o Padrão de Projeto Facade:

1. Crie uma instância da classe `Facade`.
2. Passe essa instância para o código do cliente.
3. O código do cliente chama os métodos da fachada, que internamente coordenam as operações dos subsistemas.

Exemplo:

```typescript
const subsystem1 = new Subsystem1();
const subsystem2 = new Subsystem2();
const facade = new Facade(subsystem1, subsystem2);
clientCode(facade);
```

### Benefícios

- Oculta a complexidade do subsistema, fornecendo uma interface simplificada para o cliente.
- Promove o desacoplamento entre o cliente e os componentes individuais do subsistema.
- Simplifica a manutenção, pois as mudanças internas no subsistema não afetam o código do cliente.

### Quando Usar

Use o Padrão de Projeto Facade quando:

- Você precisa fornecer uma interface simples para um subsistema complexo.
- Você deseja desacoplar o código do cliente dos componentes individuais do subsistema.
- Você quer reduzir a dependência do cliente em relação ao subsistema.

### Diagrama UML

![Estrutura do padrão Facade](https://refactoring.guru/images/patterns/diagrams/facade/structure.png)

> **Material usado:** https://refactoring.guru/pt-br/design-patterns/facade

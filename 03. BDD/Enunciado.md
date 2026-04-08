# 🍔 Exercício BDD – Hamburgueria 

## Orientações 
- Faça **em dupla ou trio**.
## 🎯 Objetivo
- **Completar no arquivo `.feature`** os cenários.
- **Implementar as classes de teste** (Runner + Steps) em Java com Cucumber.
- Fazer os testes **passarem** com base nas regras de negócio.

---

## ✅ O que você vai entregar
1. `src/test/resources/features/pedidos.feature` **completo** 
2. `src/test/java/runner/RunnerTest.java`
3. `src/test/java/steps/PedidoSteps.java` (Steps em PT-BR), implementando todos os Dado/Quando/Então dos cenários.

---

## 📚 Regras de Negócio 
- Os **nomes dos itens** devem **bater exatamente** com o cardápio.
- Se um item **não existe** → “Item indisponível no cardápio”.
- Se **quantidade inválida** → “Quantidade inválida”.
- Tempo estimado = 8 (fixo) + 2 * quantidadeTotal.

## 🗂️ Estrutura (Maven)

```css
hamburgueria-bdd
├─ pom.xml
└─ src
   ├─ main
   │  └─ java
   │     └─ peppa.hamburgueria
   │        │  ├─ CardapioService.java
   │        │  └─ PedidoService.java
   └─ test
      ├─ java
      │  ├─ steps
      │  │  ├─ PedidoSteps.java
      │  └─ runner
      │     └─ RunnerTest.java
      └─ resources
         └─ features
            └─ pedidos.feature
```

## 🧪 Feature em Gherkin

```gherkin
# language: pt
@hamburgueria
Funcionalidade: Pedidos na hamburgueria Peppa Lanches
  Para realizar pedidos corretos
  Como cliente
  Eu quero saber se o item pode ser pedido, o valor total e o tempo estimado

  Contexto:
    Dado que o cardápio contém os itens:
      | item         | preco |
      | x-bacon      | 25.00 |
      | x-salada     | 22.00 |
      | batata frita | 12.00 |

  @feliz
  Cenário: Pedido simples de item existente
  ...

  @inexistente
  Cenário: Pedido de item inexistente
  ...

  @quantidade
  Cenário: Pedido com quantidade inválida
  ...

  @desconto
  Cenário: Pedido com desconto de 10 por cento
  ...
  
  @sla
  Cenário: Calcular tempo estimado de preparo
  ...
```

## 🔧 Implementação da Classe CardapioService.java
```java
public class CardapioService {
   private final Map<String, Double> precos = new HashMap<>();

    public void cadastrarItem(String nome, double preco) {
        precos.put(nome, preco);
    }

    public boolean existe(String nome) {
        return precos.containsKey(nome);
    }

    public double precoDe(String nome) {
        return precos.getOrDefault(nome, 0.0);
    }
}
```
## 🔧 Implementação da Classe PedidoService.java
```java
public class PedidoService {
  private final CardapioService cardapio;

    public PedidoService(CardapioService cardapio) {
        this.cardapio = cardapio;
    }

    public double calcularTotal(String item, int quantidade) {
        if (!cardapio.existe(item)) {
            throw new IllegalArgumentException("Item indisponível no cardápio");
        }
        if (quantidade <= 0) {
            throw new IllegalArgumentException("Quantidade inválida");
        }
        double preco = cardapio.precoDe(item);
        double total = preco * quantidade;
        return Math.round(total * 100.0) / 100.0;
    }

    public int calcularTempoEstimado(int quantidadeTotal) {
        return 8 + 2 * quantidadeTotal;
    }
}
```

## Dependências pom.xml

```xml
<properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>21</maven.compiler.source>
        <maven.compiler.target>21</maven.compiler.target>
        <cucumber.version>7.20.1</cucumber.version>
        <junit.jupiter.version>5.11.3</junit.jupiter.version>
        <junit.platform.version>1.11.3</junit.platform.version>
    </properties>
    <dependencies>
        <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-java</artifactId>
        <version>${cucumber.version}</version>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-junit-platform-engine</artifactId>
        <version>${cucumber.version}</version>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>org.junit.platform</groupId>
        <artifactId>junit-platform-suite</artifactId>
        <version>${junit.platform.version}</version>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>${junit.jupiter.version}</version>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>org.junit.platform</groupId>
        <artifactId>junit-platform-suite-api</artifactId>
        <version>${junit.platform.version}</version>
        <scope>test</scope>
        <type>jar</type>
    </dependency>
    </dependencies>
```
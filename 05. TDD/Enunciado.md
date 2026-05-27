# 🧪 Exercícios de TDD com Java e JUnit


A proposta é desenvolver as soluções seguindo o ciclo:

```text
Red → Green → Refactor
```

Ou seja:

1. **Red** — escrever um teste que falha.
2. **Green** — escrever o código mínimo para o teste passar.
3. **Refactor** — melhorar o código sem quebrar os testes.

---

# ✅ Exercício 1 — Calculadora de Desconto para Loja

A loja fictícia **TechStore** está desenvolvendo um sistema simples para calcular automaticamente o valor final de uma compra após a aplicação de descontos.

Atualmente, os vendedores calculam os descontos manualmente, o que pode gerar erros, principalmente em períodos de promoção. Para evitar inconsistências, a empresa decidiu criar uma funcionalidade que receba o valor total da compra e retorne o valor final que o cliente deverá pagar.

A regra de negócio definida pela loja é baseada no valor total da compra:

| Valor total da compra | Desconto aplicado |
|---|---:|
| Menor que R$ 100,00 | Sem desconto |
| De R$ 100,00 até R$ 499,99 | 5% de desconto |
| A partir de R$ 500,00 | 10% de desconto |

Além disso, o sistema deve impedir cálculos com valores inválidos. Portanto, caso o valor da compra seja negativo, o sistema deve lançar uma exceção do tipo `IllegalArgumentException`.

---

## 🧩 Requisitos funcionais

A classe deverá se chamar:

```java
CalculadoraDesconto
```

Ela deverá possuir o método:

```java
public double calcularValorFinal(double valorCompra)
```

Esse método deverá:

1. Receber o valor total da compra.
2. Verificar se o valor é válido.
3. Aplicar o percentual de desconto correto.
4. Retornar o valor final da compra já com o desconto aplicado.

---

## 📋 Regras de negócio

### Regra 1 — Compra abaixo de R$ 100,00

Quando o valor da compra for menor que R$ 100,00, nenhum desconto deverá ser aplicado.

Exemplo:

```text
Entrada: 80.00
Saída esperada: 80.00
```

---

### Regra 2 — Compra entre R$ 100,00 e R$ 499,99

Quando o valor da compra for maior ou igual a R$ 100,00 e menor que R$ 500,00, deverá ser aplicado desconto de 5%.

Exemplo:

```text
Entrada: 200.00
Cálculo: 200 - 5% = 190.00
Saída esperada: 190.00
```

---

### Regra 3 — Compra a partir de R$ 500,00

Quando o valor da compra for maior ou igual a R$ 500,00, deverá ser aplicado desconto de 10%.

Exemplo:

```text
Entrada: 1000.00
Cálculo: 1000 - 10% = 900.00
Saída esperada: 900.00
```

---

### Regra 4 — Valor negativo

O sistema não deve aceitar valores negativos.

Exemplo:

```text
Entrada: -50.00
Resultado esperado: IllegalArgumentException
```

---

Os testes devem ser criados gradualmente. Por exemplo:

1. Primeiro, testar compra abaixo de R$ 100,00.
2. Depois, testar compra com desconto de 5%.
3. Depois, testar compra com desconto de 10%.
4. Depois, testar valores-limite, como R$ 100,00 e R$ 500,00.
5. Por fim, testar valor negativo.
---

# ✅ Exercício 2 — Classificador de Situação de Alunos


A escola fictícia **Escola Futuro Digital** deseja automatizar a classificação da situação final de seus alunos ao término do semestre.

Atualmente, a secretaria faz essa classificação manualmente consultando a nota final e a frequência de cada estudante. Esse processo pode gerar erros, principalmente quando há muitos alunos para avaliar.

Para melhorar esse fluxo, a escola decidiu criar uma classe responsável por classificar automaticamente o aluno com base em dois dados:

- Nota final.
- Frequência percentual.

A nota final representa o desempenho acadêmico do aluno, variando de `0` a `10`.

A frequência representa o percentual de presença nas aulas, variando de `0` a `100`.

A classificação do aluno deverá seguir as regras estabelecidas pela escola.

---

## 🧩 Requisitos funcionais

A classe deverá se chamar:

```java
ClassificadorAluno
```

Ela deverá possuir o método:

```java
public String classificar(double notaFinal, double frequencia)
```

Esse método deverá:

1. Receber a nota final do aluno.
2. Receber a frequência percentual do aluno.
3. Validar se os valores informados são permitidos.
4. Classificar a situação do aluno.
5. Retornar uma mensagem textual com a situação final.

---

## 📋 Regras de negócio

| Nota final | Frequência | Situação |
|---:|---:|---|
| Nota maior ou igual a 7,0 | Frequência maior ou igual a 75% | Aprovado |
| Nota maior ou igual a 5,0 e menor que 7,0 | Frequência maior ou igual a 75% | Recuperação |
| Nota menor que 5,0 | Frequência maior ou igual a 75% | Reprovado por nota |
| Qualquer nota válida | Frequência menor que 75% | Reprovado por frequência |

---

## ⚠️ Regras de validação

O sistema deve validar os dados de entrada antes de classificar o aluno.

### Nota inválida

A nota final deve estar entre `0` e `10`.

São exemplos de notas inválidas:

```text
-1
11
15
```

Caso a nota seja inválida, o sistema deve lançar:

```java
IllegalArgumentException
```

---

### Frequência inválida

A frequência deve estar entre `0` e `100`.

São exemplos de frequências inválidas:

```text
-10
120
150
```

Caso a frequência seja inválida, o sistema deve lançar:

```java
IllegalArgumentException
```

---

## 🧪 Exemplos de funcionamento

### Exemplo 1 — Aluno aprovado

```text
Entrada:
notaFinal = 8.0
frequencia = 90.0

Saída esperada:
Aprovado
```

---

### Exemplo 2 — Aluno em recuperação

```text
Entrada:
notaFinal = 6.0
frequencia = 80.0

Saída esperada:
Recuperação
```

---

### Exemplo 3 — Aluno reprovado por nota

```text
Entrada:
notaFinal = 4.0
frequencia = 90.0

Saída esperada:
Reprovado por nota
```

---

### Exemplo 4 — Aluno reprovado por frequência

```text
Entrada:
notaFinal = 9.0
frequencia = 60.0

Saída esperada:
Reprovado por frequência
```

---

Sugestão de ordem:

1. Criar teste para aluno aprovado.
2. Criar teste para aluno em recuperação.
3. Criar teste para aluno reprovado por nota.
4. Criar teste para aluno reprovado por frequência.
5. Criar testes para valores-limite:
   - nota exatamente 7.0;
   - nota exatamente 5.0;
   - frequência exatamente 75.0.
6. Criar testes para nota inválida.
7. Criar testes para frequência inválida.
8. Refatorar o código usando constantes e métodos auxiliares.

---

# 📦 Dependência JUnit 5 no `pom.xml`

```xml
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>5.11.3</version>
        <scope>test</scope>
    </dependency>
</dependencies>

<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.2.5</version>
        </plugin>
    </plugins>
</build>
```

---

# ✅ Comando para executar os testes

No terminal, execute:

```bash
mvn test
```
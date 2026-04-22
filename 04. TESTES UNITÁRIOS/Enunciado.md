# 🧾 Exercício — Gerenciamento de Clientes e Contas Bancárias (Java + JUnit 5 + Suite)

> **Objetivo:** implementar um mini–sistema bancário (clientes e contas) e cobrir as regras com **testes unitários** (JUnit 5), organizados em **suites**.  

---

## 🏦 Domínio & Regras de Negócio

### Entidades
- **Cliente**
  - `id` (UUID/String), `nome` (não vazio), `cpf` (11 dígitos), `contas` (lista somente leitura).
- **Conta** (abstrata)
  - `numero` (String), `titular` (Cliente), `saldo` (BigDecimal ≥ 0).
  - Operações: `depositar(valor)`, `sacar(valor)`, `transferir(destino, valor)`.
  - **Validações gerais**:
    - `valor` deve ser `> 0` (senão `ValorInvalidoException`).
    - `sacar/transferir` não podem exceder saldo (senão `SaldoInsuficienteException`).
- **ContaCorrente** (extends Conta)
  - **Tarifa de saque:** **R$ 1,00** por operação (`saldo >= valor + 1`).
- **ContaPoupanca** (extends Conta)
  - **Sem tarifa** em `sacar`.  
  - **Rendimento mensal:** `render(taxaPercentualMensal)`; taxa `>= 0`.

### Exceções
- `ValorInvalidoException` — valores `≤ 0` ou taxa negativa.  
- `SaldoInsuficienteException` — saldo não cobre a operação.  
- `ClienteNaoEncontradoException` — busca de cliente inexistente.  
- `ContaNaoEncontradaException` - ao procurar conta por número.

---

## 🧱 Estrutura de Projeto (Maven)

```bash
banco/
│── pom.xml
├── src/
│   ├── main/java/com/example/banco/
│   │   ├── dominio/
│   │   │   ├── Cliente.java
│   │   │   ├── Conta.java
│   │   │   ├── ContaCorrente.java
│   │   │   └── ContaPoupanca.java
│   │   ├── excecoes/
│   │   │   ├── ValorInvalidoException.java
│   │   │   ├── SaldoInsuficienteException.java
│   │   │   └── ClienteNaoEncontradoException.java
│   │   └── servico/
│   │       └── BancoService.java
│   └── test/java/com/example/banco/
│       ├── dominio/
│       │   ├── ContaCorrenteTest.java
│       │   ├── ContaPoupancaTest.java
│       │   └── ClienteTest.java
│       ├── servico/
│       │   └── BancoServiceTest.java
│       └── suite/
│           └── BancoAllTestsSuite.java
```

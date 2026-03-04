# Sistema de Gerenciamento de Provas

Uma escola precisa de um sistema simples para montar uma prova com diferentes tipos de questões e corrigir automaticamente as respostas de um aluno.

## Requisitos obrigatórios

### 1) Interface Corrigivel

Crie a interface:

- double corrigir(String respostaDoAluno);

Todo tipo de questão precisa “saber” se a resposta está correta e quantos pontos vale.

### 2) Classe abstrata Questao

Crie uma classe abstrata Questao que implementa Corrigivel e possui:

- String enunciado

- double peso

### 3) Subclasses

Implemente dois tipos de questão:

- QuestaoMultiplaEscolha

    Atributos:
    
    - List<String> alternativas
    
    - String gabarito (ex.: "A", "B", "C", "D")
    
    Correção:
    
    - se a resposta do aluno for igual ao gabarito → retorna peso
    
    - caso contrário → retorna 0

- QuestaoVerdadeiroFalso

    Atributo:
    
    - boolean gabarito
    
    Entrada esperada:
    
    - "V" ou "F" (aceite também "true" / "false" se quiser)
    
    Correção:
    
    - se bater com o gabarito → retorna peso
    
    - senão → 0

### 4) Classe Prova

Crie a classe Prova com:

- String titulo

- List<Questao> questoes

Métodos obrigatórios:

- void adicionarQuestao(Questao q)

- double valorTotal() (soma dos pesos)

- double corrigirProva(List<String> respostas)

⚠️ Regra:

- O número de respostas deve ser igual ao número de questões.

### 5) Classe ProvasApp

Crie a classe ProvasApp com o main e um menu:

1) Listar questões
2) Responder e corrigir prova
0) Sair

Regras:

- A prova deve ser criada e preenchida automaticamente com pelo menos 1 questão de múltipla escolha e 1 de verdadeiro/falso ao iniciar o programa.

- Ao escolher “Responder e corrigir”, o programa deve pedir a resposta do aluno para cada questão e ao final exibir:

   - nota por questão

   - nota total

   - valor total da prova

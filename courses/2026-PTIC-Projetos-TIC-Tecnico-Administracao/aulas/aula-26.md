---
layout: aula
title: "Aula 26 - Lógica: Decisão (Se/Então)"
date: 2026-06-16
category: aulas
course_id: ptic
---

# Aula 26 - Lógica: Decisão (Se/Então)

**Data:** 16/06/2026  
**Duração:** 1 hora-aula (50 min) **Local:** Laboratório de Informática  
**Objetivo:** Compreender e aplicar a estrutura de decisão (condicional)
`Se...Então...Senao` para criar algoritmos que realizam escolhas baseadas em
critérios lógicos.

---

## 1. Abertura: O Poder do "Depende" (10 minutos)

### A Inteligência da Escolha

Na vida e na administração, poucas coisas são diretas. Quase tudo depende de uma
condição. "Se o estoque for baixo, compre mais". "Se o aluno tiver média acima
de 6, está aprovado". Essa é a base da inteligência artificial e da automação.

### Guia para o Professor

- **Instruções Didáticas:** Pergunte aos alunos sobre decisões do dia a dia: "O
  que você faz se o despertador não tocar?". Mostre que o cérebro humano está o
  tempo todo processando condições.
- **Perguntas para a Turma:**
  - "O computador consegue tomar decisões sozinho ou ele apenas segue as
    condições que nós definimos?"
  - "O que aconteceria se um sistema de banco não tivesse uma estrutura de
    decisão para o saldo da conta?"
- **Dicas de Condução:** Conecte esta aula com a Aula 18 (Função SE nas
  planilhas). Mostre que a lógica é a mesma, só muda a forma de escrever.

---

## 2. Teoria: A Sintaxe da Condição (15 minutos)

### O Fluxo de Decisão

No PSeInt, a estrutura é:

```
Se [Teste Lógico] Entao
   [Ação se for verdade]
Senao
   [Ação se for falso]
FimSe
```

- **Operadores Relacionais:** `>` (Maior), `<` (Menor), `>=` (Maior ou igual),
  `<=` (Menor ou igual), `=` (Igual), `<>` (Diferente).

### Guia para o Professor

- **Instruções Didáticas:** Demonstre um exemplo simples: verificar se uma
  pessoa é maior de idade. Mostre a importância de indentar o código (colocar os
  comandos um pouco mais para a direita dentro do `Se`) para facilitar a
  leitura.
- **Perguntas para a Turma:**
  - "Para que serve o `Senao`?"
  - "O que acontece se eu esquecer o `FimSe` no final do bloco?"
- **Dicas de Condução:** Use o desenho do losango no fluxograma para representar
  o `Se...Entao`.

---

## 3. Atividade Prática

Os alunos devem criar um programa que:

1. Peça o nome do cliente.
2. Peça o valor do salário do cliente.
3. Peça o valor da parcela do empréstimo pretendido.
4. **Condição:** Se o valor da parcela for maior que 30% do salário, o crédito é
   "REPROVADO". Caso contrário, é "APROVADO".
5. O programa deve mostrar a decisão final na tela.

### Guia para o Professor

- **Instruções Didáticas:** Ajude no cálculo da porcentagem dentro do teste
  lógico: `Se parcela > (salario * 0.3) Entao`. Circule verificando se eles
  estão fechando as aspas e os parênteses.
- **Perguntas para a Turma:**
  - "Qual mensagem seu programa daria se a parcela fosse exatamente 30% do
    salário?"
  - "Como você alteraria o código para avisar que o valor do salário não pode
    ser zero?"
- **Dicas de Condução:** Mostre como usar "Mensagens Amigáveis" nos dois
  caminhos (Sim e Não) para tornar o sistema mais profissional.

### Entrega

- Registrar a atividade no [Formulário da Aula 26](formulario-aula-26).
- Anexar ou informar o link do arquivo, pasta, apresentação ou evidência
  produzida.
- Manter o portfólio organizado com nome de arquivo coerente e data da aula.---

## 4. Estrutura do Formulário (Google Forms)

| Ordem | Pergunta                                          | Tipo de Resposta | Observação                             |
| :---: | :------------------------------------------------ | :--------------- | :------------------------------------- |
|   1   | Nome Completo                                     | Resposta curta   | Obrigatório                            |
|   2   | Qual o operador usado para 'Diferente' em lógica? | Múltipla escolha | <>                                     |
|   3   | O bloco 'Senao' é executado em qual situação?     | Múltipla escolha | Quando o teste lógico é Falso          |
|   4   | Por que a indentação é importante no código?      | Múltipla escolha | Para facilitar a leitura e organização |

---

## 5. Dicas de Ouro para o Professor

1. **Testes de Mesa:** Ensine o aluno a fazer o "Teste de Mesa" (simular o
   código no papel com valores diferentes). Ex: O que acontece se eu digitar
   1000 reais de salário e 500 de parcela?
2. **Operador Igual:** Cuidado com a confusão entre o símbolo de atribuição
   (seta ou igual em algumas linguagens) e o símbolo de comparação. No PSeInt,
   `=` compara se dois valores são iguais.
3. **Múltiplas Condições:** Para alunos avançados, introduza o `E` e o `OU`. Ex:
   `Se (salario > 0) E (parcela > 0) Entao...`.

---

## 6. Anexos e Referências

- **Materiais:**
  [Estruturas de Decisão no Pseudocódigo](/self/courses/2026-PTIC-Projetos-TIC-Tecnico-Administracao/materiais/material-09)
  [Atividade 26 - Lógica: Decisão (Se/Então)](/self/courses/2026-PTIC-Projetos-TIC-Tecnico-Administracao/atividades/atividade-26)
- **Links Úteis:**
  [Aprenda Lógica de Programação - Estruturas Condicionais](https://www.youtube.com/watch?v=A_0nfmYFz-k)

---

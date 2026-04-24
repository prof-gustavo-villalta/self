---
layout: aula
title: "Aula 27 - Lógica: Repetição"
date: 2026-06-20
category: aulas
course_id: ptic
---

# Aula 27 - Lógica: Repetição

**Data:** 20/06/2026 (Sábado Letivo)  
**Duração:** 1 hora-aula (50 min) **Local:** Laboratório de Informática  
**Objetivo:** Compreender e aplicar estruturas de repetição (loops) para
automatizar tarefas repetitivas em algoritmos.

---

## 1. Abertura: O Poder da Automação (10 minutos)

### Por que repetir?

Na administração, muitas tarefas são repetitivas: processar uma folha de
pagamento com 100 funcionários, verificar o estoque de 500 itens ou enviar
e-mails de cobrança. Se o computador sabe fazer uma vez, ele pode fazer mil
vezes sem cansar ou errar.

### Guia para o Professor

- **Instruções Didáticas:** Peça para um aluno escrever o nome dele 10 vezes no
  quadro. Depois, mostre como um comando de repetição faria isso em
  milissegundos.
- **Perguntas para a Turma:**
  - "Qual tarefa na escola ou no trabalho você acha mais chata por ser
    repetitiva?"
  - "Como o computador sabe quando parar de repetir?"
- **Dicas de Condução:** Use a analogia do despertador que toca a cada 5 minutos
  (soneca) até você levantar.

---

## 2. Teoria: Enquanto e Para (15 minutos)

### Estruturas de Loop no PSeInt

1. **Para (For):** Usado quando sabemos exatamente quantas vezes repetir.
   ```
   Para i de 1 ate 10 faca
      Escreva("Contagem: ", i)
   FimPara
   ```
2. **Enquanto (While):** Usado quando a repetição depende de uma condição (não
   sabemos o total exato).
   ```
   Enquanto (saldo > 0) faca
      [Ação de gastar]
   FimEnquanto
   ```

### Guia para o Professor

- **Instruções Didáticas:** Explique o conceito de "Variável de Controle" (o `i`
  no Para). Mostre que ela funciona como um contador de voltas em uma pista.
- **Perguntas para a Turma:**
  - "Se eu colocar `Para i de 10 ate 1`, o que acontece?"
  - "O que é um 'Loop Infinito' e por que ele é perigoso?"
- **Dicas de Condução:** Desenhe o fluxo no quadro mostrando a "volta" que a
  seta faz no fluxograma.

---

## 3. Atividade Prática

Os alunos devem criar um programa que:

1. Pergunte quantos alunos existem na sala.
2. Use um laço `Para` para pedir a nota de cada aluno.
3. Vá somando essas notas em uma variável `soma`.
4. Ao final do laço, calcule a média (soma / total de alunos) e exiba o
   resultado.

### Guia para o Professor

- **Instruções Didáticas:** Introduza o conceito de **Acumulador**
  (`soma = soma + nota`). É uma das lógicas mais difíceis para iniciantes. Use a
  analogia de um cofrinho.
- **Perguntas para a Turma:**
  - "Por que precisamos zerar a variável `soma` antes de começar o Para?"
  - "Como o programa mudaria se quiséssemos parar de pedir notas apenas quando
    digitássemos -1?"
- **Dicas de Condução:** Circule pela sala ajudando na sintaxe do PSeInt,
  especialmente no `FimPara`.

### Entrega

- Registrar a atividade no [Formulário da Aula 27](formulario-aula-27).
- Anexar ou informar o link do arquivo, pasta, apresentação ou evidência
  produzida.
- Manter o portfólio organizado com nome de arquivo coerente e data da aula.---

## 4. Estrutura do Formulário (Google Forms)

| Ordem | Pergunta                                                               | Tipo de Resposta | Observação                                |
| :---: | :--------------------------------------------------------------------- | :--------------- | :---------------------------------------- |
|   1   | Nome Completo                                                          | Resposta curta   | Obrigatório                               |
|   2   | Qual estrutura de repetição é melhor quando sabemos o número de vezes? | Múltipla escolha | Para (For)                                |
|   3   | O que acontece se a condição de um 'Enquanto' nunca for falsa?         | Múltipla escolha | Loop Infinito                             |
|   4   | O que é um 'Acumulador' em programação?                                | Múltipla escolha | Uma variável que guarda a soma de valores |

---

## 5. Dicas de Ouro para o Professor

1. **Loop Infinito:** Se o computador "travar", mostre como interromper a
   execução no PSeInt (botão Parar).
2. **Visualização:** Use o modo "Passo a Passo" do PSeInt para que o aluno veja
   a "luzinha" voltando para o início do loop.
3. **Desafio:** Para os mais rápidos, peça para contar quantos alunos foram
   aprovados (usando um `Se` dentro do `Para`).

---

## 6. Anexos e Referências

- **Materiais:**
  [Guia de Estruturas de Repetição](/self/courses/2026-PTIC-Projetos-TIC-Tecnico-Administracao/materiais/material-10)
- **Links Úteis:**
  [Lógica de Programação: Estruturas de Repetição](https://www.youtube.com/watch?v=U57gU_K_vto)

---

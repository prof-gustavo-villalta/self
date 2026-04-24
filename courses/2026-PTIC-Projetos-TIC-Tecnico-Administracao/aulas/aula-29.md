---
layout: aula
title: "Aula 29 - Algoritmos em Adm"
date: 2026-06-23
category: aulas
course_id: ptic
---

# Aula 29 - Algoritmos em Adm

**Data:** 23/06/2026  
**Duração:** 1 hora-aula (50 min) **Local:** Laboratório de Informática  
**Objetivo:** Aplicar lógica de programação em processos administrativos reais,
desenvolvendo algoritmos para tomada de decisão e controle.

---

## 1. Abertura: O Algoritmo por Trás da Empresa (10 minutos)

### Gestão é Lógica

Uma empresa é um grande conjunto de algoritmos. "Se o cliente pagou, libere o
pedido". "Se o funcionário fez hora extra, calcule o adicional". Hoje, vamos
tirar a lógica do papel e transformar em automação administrativa.

### Guia para o Professor

- **Instruções Didáticas:** Apresente um fluxograma de um processo de compras
  simples. Mostre como cada etapa do fluxograma se traduz em um comando de
  programação.
- **Perguntas para a Turma:**
  - "Qual processo na ETEC vocês acham que segue uma lógica bem clara?" (Ex:
    Matrícula, empréstimo de livros).
  - "O que acontece se um passo do processo for pulado?"
- **Dicas de Condução:** Use exemplos do cotidiano administrativo para gerar
  identificação.

---

## 2. Teoria: Variáveis de Negócio (15 minutos)

### Tipos de Dados na Administração

- **Inteiro:** Quantidade de produtos em estoque, número de funcionários.
- **Real:** Preços, salários, alíquotas de impostos.
- **Cadeia (String):** Nomes de clientes, endereços, descrições de produtos.
- **Lógico:** Status de pagamento (Pago/Pendente), Disponibilidade (Sim/Não).

### Guia para o Professor

- **Instruções Didáticas:** Explique que escolher o tipo certo de dado economiza
  memória e evita erros. Não se soma nomes, não se escreve "vencido" em uma
  variável de data.
- **Perguntas para a Turma:**
  - "Qual o melhor tipo de dado para um CPF?" (Resposta: Cadeia, pois não
    faremos cálculos e tem zeros à esquerda).
  - "E para o saldo de uma conta bancária?" (Resposta: Real).
- **Dicas de Condução:** Faça um exercício rápido de classificação de dados no
  quadro.

---

## 3. Atividade Prática

Os alunos devem desenvolver um algoritmo (no PSeInt ou Scratch) que:

1. Receba o valor total da compra.
2. Aplique a regra de negócio:
   - Se valor < 100: Sem desconto.
   - Se valor entre 100 e 500: 5% de desconto.
   - Se valor > 500: 10% de desconto.
3. Exiba o valor do desconto e o valor final a pagar.

### Guia para o Professor

- **Instruções Didáticas:** Ajude na construção das condições compostas:
  `Se valor >= 100 E valor <= 500 Entao`.
- **Perguntas para a Turma:**
  - "Por que é importante testar o programa com valores de 'fronteira' (ex:
    99.99, 100.00, 500.00)?"
  - "Como você adicionaria uma mensagem de 'Cliente VIP' para quem ganha o
    desconto máximo?"
- **Dicas de Condução:** Incentive os alunos a criarem uma interface amigável
  ("Bem-vindo ao Sistema de Vendas").

### Entrega

- Registrar a atividade no [Formulário da Aula 29](formulario-aula-29).
- Anexar ou informar o link do arquivo, pasta, apresentação ou evidência
  produzida.
- Manter o portfólio organizado com nome de arquivo coerente e data da aula.---

## 4. Estrutura do Formulário (Google Forms)

| Ordem | Pergunta                                                        | Tipo de Resposta | Observação                                                         |
| :---: | :-------------------------------------------------------------- | :--------------- | :----------------------------------------------------------------- |
|   1   | Nome Completo                                                   | Resposta curta   | Obrigatório                                                        |
|   2   | Qual tipo de dado é ideal para armazenar o preço de um produto? | Múltipla escolha | Real                                                               |
|   3   | Na lógica `Se valor > 500`, o valor 500 entra na condição?      | Múltipla escolha | Não (apenas maiores que 500)                                       |
|   4   | Para que serve o operador 'E' em uma condição?                  | Múltipla escolha | Para exigir que as duas condições sejam verdadeiras ao mesmo tempo |

---

## 5. Dicas de Ouro para o Professor

1. **Contexto:** Lembre os alunos que no Excel eles usavam a função `SE`. Mostre
   que aqui a lógica é idêntica, apenas a "roupagem" mudou.
2. **Erros de Tipagem:** É comum tentarem calcular com variáveis de texto.
   Mostre o erro que o PSeInt gera.
3. **Modularização:** Para alunos avançados, sugira perguntar se o cliente tem
   cupom de desconto antes de aplicar a regra.

---

## 6. Anexos e Referências

- **Materiais:**
  [Algoritmos Administrativos Comuns](/self/courses/2026-PTIC-Projetos-TIC-Tecnico-Administracao/materiais/material-12)
- **Links Úteis:**
  [Lógica Aplicada a Processos de Negócio](https://www.youtube.com/watch?v=XpM_58v9_f8)

---

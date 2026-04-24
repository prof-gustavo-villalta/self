---
layout: aula
title: "Aula 18 - Exercício: Automação Simples"
date: 2026-05-25
category: aulas
course_id: ptic
---

# Aula 18 - Exercício: Automação Simples

**Data:** 25/05/2026  
**Duração:** 1 hora-aula (50 min) **Local:** Laboratório de Informática  
**Objetivo:** Consolidar o uso de planilhas para automatizar rotinas
administrativas, aplicando funções de busca e lógica básica para controle de
fluxos.

---

## 1. Abertura: O Poder da Automação (10 minutos)

### Por que automatizar?

Automação não é apenas para robôs em fábricas. Na administração, automatizar
significa fazer com que a planilha tome decisões simples por você, como avisar
quando um estoque está baixo ou quando uma conta está vencida.

### Guia para o Professor

- **Instruções Didáticas:** Lance um desafio: mostre uma lista de 50 alunos com
  médias e pergunte se é viável escrever "Aprovado" ou "Reprovado" um por um.
  Introduza o conceito de que o computador pode fazer isso em milissegundos.
- **Perguntas para a Turma:**
  - "Qual o risco de preencher manualmente o status de 500 pedidos de uma loja
    virtual?"
  - "O que você faria com o tempo que ganharia se suas planilhas se preenchessem
    sozinhas?"
- **Dicas de Condução:** Explique que a automação reduz a fadiga do trabalho
  repetitivo e permite que o profissional foque em tarefas que exigem
  criatividade e decisão humana.

---

## 2. Teoria: A Lógica da Condição SE (15 minutos)

### O Se Então (IF Then)

- **A Função SE:** `=SE(Teste_Lógico; Valor_se_Verdadeiro; Valor_se_Falso)`.
- **Exemplo prático:** `=SE(A1>=6; "APROVADO"; "REPROVADO")`.
- **Formatação Condicional:** Mudar a cor da célula automaticamente (Ex:
  Vermelho se estiver negativo).

### Guia para o Professor

- **Instruções Didáticas:** Demonstre a sintaxe da função SE no projetor. Mostre
  como aplicar a "Formatação Condicional" (`Formatar > Formatação Condicional`)
  para pintar de azul os valores positivos e de vermelho os negativos.
- **Perguntas para a Turma:**
  - "Se o saldo da minha conta for exatamente zero, o que apareceria na função
    `=SE(Saldo>0; "Lucro"; "Prejuízo")`?"
  - "Como a cor ajuda o gestor a tomar uma decisão rápida sem precisar ler o
    número?"
- **Dicas de Condução:** Reforce que no Excel/Sheets, textos dentro de fórmulas
  devem estar sempre entre aspas duplas `" "`.

---

## 3. Atividade Prática

Os alunos devem criar uma planilha de controle de estoque que:

1. Calcule o Estoque Atual (Entradas - Saídas).
2. Use a função `=SE()` para mostrar "REPOR ESTOQUE" se o saldo for menor que 5
   unidades.
3. Aplique formatação condicional vermelha para os itens que precisam de
   reposição.
4. Use `=SOMA()` para o valor total investido em estoque.

### Guia para o Professor

- **Instruções Didáticas:** Circule pelo laboratório e ajude os alunos a
  montarem a lógica da subtração antes de aplicarem o SE.
- **Perguntas para a Turma:**
  - "Sua planilha avisou que a caneta acabou ao digitar uma saída maior que a
    entrada?"
  - "Por que o estoque mínimo é importante para uma empresa não parar de
    trabalhar?"
- **Dicas de Condução:** Desafie os alunos mais avançados a usarem o "SE
  aninhado" ou a validarem os dados para evitar saídas maiores que o estoque
  atual.

### Entrega

- Registrar a atividade no [Formulário da Aula 18](formulario-aula-18).
- Anexar ou informar o link do arquivo, pasta, apresentação ou evidência
  produzida.
- Manter o portfólio organizado com nome de arquivo coerente e data da aula.---

## 4. Estrutura do Formulário (Google Forms)

| Ordem | Pergunta                                       | Tipo de Resposta | Observação                           |
| :---: | :--------------------------------------------- | :--------------- | :----------------------------------- |
|   1   | Nome Completo                                  | Resposta curta   | Obrigatório                          |
|   2   | Para que serve a função =SE()?                 | Múltipla escolha | Para realizar testes lógicos         |
|   3   | O que é Formatação Condicional?                | Múltipla escolha | Alteração de estilo baseada no valor |
|   4   | Como indicamos um texto dentro de uma fórmula? | Múltipla escolha | Entre aspas duplas (" ")             |

---

## 5. Dicas de Ouro para o Professor

1. **Lógica Primeiro:** Peça para os alunos escreverem a lógica no papel (em
   português) antes de digitarem a fórmula. Ex: "Se a média for maior que 6,
   escreva aprovado".
2. **Cuidado com o Ponto e Vírgula:** Muitos alunos usam vírgula para separar os
   termos da função. Reforce que no padrão brasileiro do Excel/Sheets, o
   separador é o ponto e vírgula `;`.
3. **Visualização Rápida:** Ensine que a automação visual (cores) é tão
   importante quanto a automação lógica (fórmulas), pois ajuda o cérebro humano
   a processar o alerta mais rápido.

---

## 6. Anexos e Referências

- **Materiais:**
  [Automação Básica com Fórmulas Lógicas](/self/courses/2026-PTIC-Projetos-TIC-Tecnico-Administracao/materiais/material-08)
  [Atividade 18 - Exercício: Automação Simples](/self/courses/2026-PTIC-Projetos-TIC-Tecnico-Administracao/atividades/atividade-18)
- **Links Úteis:**
  [Como usar a função SE no Google Sheets](https://support.google.com/docs/answer/3093364)

---

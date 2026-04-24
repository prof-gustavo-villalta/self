---
layout: aula
title: "Aula 17 - Planilhas: Fórmulas Básicas"
date: 2026-05-19
category: aulas
course_id: ptic
---

# Aula 17 - Planilhas: Fórmulas Básicas

**Data:** 19/05/2026  
**Duração:** 1 hora-aula (50 min)  
**Local:** Laboratório de Informática  
**Objetivo:** Compreender a lógica das fórmulas e funções, aplicando cálculos de
soma, média e multiplicação em contextos administrativos.

---

## 1. Conteúdo Teórico: O Igual que Faz Mágica

Uma planilha só começa a "pensar" quando usamos o sinal de igual (**=**). A
partir daí, ela deixa de mostrar texto e passa a processar instruções lógicas.

### Operadores e Funções

- **Operadores Matemáticos:** `+` (Soma), `-` (Subtração), `*` (Multiplicação),
  `/` (Divisão).
- **Referências de Célula:** Em vez de digitar `=10+20`, usamos `=A1+B1`. Assim,
  se o valor em A1 mudar, o resultado atualiza sozinho!
- **Funções Básicas:**
  - `=SOMA(A1:A10)`: Soma todos os valores no intervalo.
  - `=MÉDIA(B1:B10)`: Calcula a média aritmética.
  - `=MÁXIMO()` e `=MÍNIMO()`: Identificam os valores extremos.

---

## 2. Guia para o Professor (Instruções Didáticas)

### Abertura (10 minutos)

- **A Analogia das Caixas:** Explique que a célula é uma caixa. O endereço (A1)
  é a etiqueta. A fórmula olha dentro da caixa para fazer a conta.
- **Erros Comuns:** Mostre o erro `#VALOR!` (quando tentamos somar texto com
  número) e como corrigi-lo.

### Oficina Prática (35 minutos)

- **Foco:** Ajude os alunos a usarem a **Alça de Preenchimento** para arrastar
  fórmulas de multiplicação (Preço x Quantidade) para a lista toda.
- **Dica:** Ensine o uso do ponto e vírgula (`;` para e) versus dois pontos (`:`
  para até).

---

## 3. Atividade Prática: Planilha de Orçamento Adm

Use a tabela criada na aula anterior (ou crie uma nova) e adicione inteligência
a ela.

### Passo a Passo:

1. **Multiplicação:** Crie uma nova coluna chamada **Valor Total**. Use uma
   fórmula para calcular `Quantidade * Preço Unitário` para cada item.
2. **Soma Total:** No final da tabela, use a função `=SOMA()` para calcular o
   valor total de todo o estoque.
3. **Estatísticas:** Use as funções `=MÉDIA()`, `=MÁXIMO()` e `=MÍNIMO()` para
   descobrir:
   - Qual o preço médio dos itens.
   - Qual o item mais caro.
   - Qual o item mais barato.

### Critérios de Sucesso:

- Fórmulas aplicadas corretamente (usando referências de células).
- Resultado automático ao alterar uma quantidade.
- **Link de Entrega:** [Formulário da Aula 17](../atividades/formulario-aula-17)

---

## 🔗 Links e Recursos

- **Google Sheets:** [sheets.google.com](https://sheets.google.com)
- **Suporte:**
  [Lista de Funções do Google Sheets](https://support.google.com/docs/table/25273)

---

**Material elaborado para PTIC - 2026**  
Prof. Gustavo Villalta

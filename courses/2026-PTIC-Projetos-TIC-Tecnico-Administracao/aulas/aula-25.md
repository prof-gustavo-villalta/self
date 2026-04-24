---
layout: aula
title: "Aula 25 - Lógica: PSeInt e Variáveis"
date: 2026-06-15
category: aulas
course_id: ptic
---

# Aula 25 - Lógica: PSeInt e Variáveis

**Data:** 15/06/2026  
**Duração:** 1 hora-aula (50 min) **Local:** Laboratório de Informática  
**Objetivo:** Introduzir o conceito de algoritmos e variáveis utilizando a
ferramenta PSeInt (Portuñol) para exercitar a lógica de programação de forma
intuitiva.

---

## 1. Abertura: A Receita do Algoritmo (10 minutos)

### A Linguagem das Instruções

Um algoritmo é uma sequência de instruções que o computador segue para realizar
uma tarefa. Na administração, isso pode ser o cálculo de uma folha de pagamento
ou a triagem de um currículo. Para o computador entender, precisamos ser
específicos.

### Guia para o Professor

- **Instruções Didáticas:** Mostre a interface do _PSeInt_. Explique que ele é
  um "tradutor" de algoritmos. Escreva o algoritmo clássico "Olá Mundo" no
  projetor e mostre como o programa o executa passo a passo.
- **Perguntas para a Turma:**
  - "O que acontece se eu esquecer de digitar uma instrução obrigatória?"
  - "Por que usamos uma linguagem próxima do português (Pseudocódigo) em vez de
    uma linguagem de programação complexa logo de início?"
- **Dicas de Condução:** Enfatize que o foco não é a "programação", mas a
  **lógica** de como os sistemas de administração funcionam por dentro.

---

## 2. Teoria: Variáveis (Gavetas de Memória) (15 minutos)

### Guardando Informação

- **O que é uma Variável?** Espaço na memória do computador para guardar dados
  que podem mudar.
- **Tipos Básicos:**
  - `Inteiro` (Ex: 10, -5).
  - `Real` (Ex: 10.50, 0.75 - preços, notas).
  - `Caracter` (Ex: "João", "AM-123" - nomes, textos).
  - `Logico` (Ex: Verdadeiro, Falso).

### Guia para o Professor

- **Instruções Didáticas:** Use a analogia de uma gaveta com uma etiqueta. Se a
  etiqueta diz "Preço", o que tem dentro é um número. Se mudarmos o conteúdo, a
  etiqueta continua a mesma. Mostre os comandos `Escrever` e `Ler` no PSeInt.
- **Perguntas para a Turma:**
  - "O que acontece se eu tentar guardar um nome de pessoa em uma variável do
    tipo Inteiro?"
  - "Por que o nome da variável não pode ter espaços ou caracteres especiais?"
- **Dicas de Condução:** Demonstre como o comando `Ler` espera a interação do
  usuário. É a ponte entre a pessoa e o sistema.

---

## 3. Atividade Prática

Os alunos devem criar no PSeInt um programa que:

1. Peça para o usuário digitar o nome do produto.
2. Peça o preço original do produto.
3. Peça a porcentagem de desconto.
4. Calcule o preço final.
5. Mostre uma mensagem final personalizada: "O produto [nome] com desconto
   custará R$ [valor]".

### Guia para o Professor

- **Instruções Didáticas:** Ajude os alunos a montarem a fórmula matemática:
  `PreçoFinal = Preço - (Preço * Desconto / 100)`. Circule e ajude na declaração
  correta das variáveis (`Definir preco Como Real`).
- **Perguntas para a Turma:**
  - "Se o desconto for zero, o preço final muda?"
  - "Seu programa funcionou quando você digitou números quebrados (ex: 10.5)?"
- **Dicas de Condução:** Mostre a função de "Fluxograma Automático" do PSeInt.
  Ele transforma o código que eles escreveram no desenho que estudamos na aula
  passada!

### Entrega

- Registrar a atividade no [Formulário da Aula 25](formulario-aula-25).
- Anexar ou informar o link do arquivo, pasta, apresentação ou evidência
  produzida.
- Manter o portfólio organizado com nome de arquivo coerente e data da aula.---

## 4. Estrutura do Formulário (Google Forms)

| Ordem | Pergunta                                                    | Tipo de Resposta | Observação                           |
| :---: | :---------------------------------------------------------- | :--------------- | :----------------------------------- |
|   1   | Nome Completo                                               | Resposta curta   | Obrigatório                          |
|   2   | O que é uma variável na lógica de programação?              | Múltipla escolha | Espaço para guardar dados na memória |
|   3   | Qual comando no PSeInt serve para mostrar um texto na tela? | Múltipla escolha | Escrever                             |
|   4   | Para que serve o tipo de dado 'Caracter'?                   | Múltipla escolha | Guardar textos e nomes               |

---

## 5. Dicas de Ouro para o Professor

1. **A Sintaxe Importa:** No PSeInt, o ponto e vírgula no final da linha é
   opcional em algumas configurações, mas ensine a usá-lo para criar o hábito
   correto.
2. **Nomes de Variáveis Semânticos:** Desestimule o uso de nomes como `x` ou
   `y`. Ensine a usar `preco_produto` ou `nome_cliente`. Isso é padrão de
   qualidade em administração e TI.
3. **Paciência com Erros:** Erros de digitação (Ex: `Escrer` em vez de
   `Escrever`) são comuns. Ensine o aluno a ler a mensagem de erro que o
   programa fornece no rodapé.

---

## 6. Anexos e Referências

- **Materiais:**
  [Introdução ao Pseudocódigo com PSeInt](/self/courses/2026-PTIC-Projetos-TIC-Tecnico-Administracao/materiais/material-09)
  [Atividade 25 - Lógica: PSeInt e Variáveis](/self/courses/2026-PTIC-Projetos-TIC-Tecnico-Administracao/atividades/atividade-25)
- **Links Úteis:**
  [PSeInt - Download e Tutoriais](http://pseint.sourceforge.net/)

---

---
layout: aula
title: "Aula 37 - Prompt Engineering"
date: 2026-08-10
category: aulas
course_id: ptic
---

# Aula 37 - Prompt Engineering

**Data:** 10/08/2026  
**Duração:** 1 hora-aula (50 min) **Local:** Laboratório de Informática  
**Objetivo:** Aprender técnicas de engenharia de prompts para obter resultados
mais precisos, relevantes e profissionais das IAs Generativas.

---

## 1. Abertura: A Arte de Perguntar (10 minutos)

### Lixo entra, lixo sai (GIGO)

Na computação, o resultado depende da qualidade da entrada. Se você fizer uma
pergunta vaga ("Faça um texto"), terá uma resposta medíocre. Se você der
contexto e instruções claras ("Escreva um contrato de estágio seguindo a lei X
para um aluno de administração"), terá uma ferramenta poderosa. Hoje, vamos
aprender a "falar" a língua das IAs.

### Guia para o Professor

- **Instruções Didáticas:** Compare dois prompts no telão: um ruim ("Dê ideias
  de marketing") e um excelente ("Você é um especialista em marketing para
  pequenas empresas. Liste 5 estratégias de baixo custo para uma padaria em
  Americana aumentar as vendas no Instagram"). Mostre a diferença nas respostas.
- **Perguntas para a Turma:**
  - "Por que a IA precisa saber 'quem ela é' (o papel dela)?"
  - "O que acontece se dermos muitas instruções contraditórias?"
- **Dicas de Condução:** Use a analogia de dar ordens para um estagiário muito
  inteligente, mas que não conhece sua empresa.

---

## 2. Teoria: A Anatomia de um Prompt (15 minutos)

### O Framework Persona-Contexto-Tarefa-Formato

Para um prompt perfeito, tente incluir:

1. **Persona (Quem):** "Atue como um Diretor de RH".
2. **Contexto (Onde/Por que):** "Estamos contratando jovens aprendizes para uma
   metalúrgica".
3. **Tarefa (O que):** "Crie 3 perguntas para a entrevista técnica".
4. **Restrições/Formato (Como):** "Use linguagem acolhedora. Responda em
   tópicos".

### Guia para o Professor

- **Instruções Didáticas:** Explique o conceito de **Few-Shot Prompting** (dar
  exemplos para a IA seguir). Se você quer que ela escreva como você, dê 2
  exemplos de textos seus antes.
- **Perguntas para a Turma:**
  - "O que são 'delimitadores' (como aspas ou hashtags) e para que servem no
    prompt?"
  - "Como pedir para a IA pensar 'passo a passo' ajuda no resultado?"
- **Dicas de Condução:** Mostre que prompts longos geralmente são melhores que
  prompts curtos.

---

## 3. Atividade Prática

Os alunos devem escolher um dos desafios abaixo e aplicar a técnica de
Persona-Contexto-Tarefa-Formato:

**Desafio A:** Criar um roteiro de atendimento para lidar com um cliente que
recebeu um produto quebrado. **Desafio B:** Escrever um anúncio de vaga de
emprego para "Assistente Administrativo" que atraia pessoas criativas. **Desafio
C:** Pedir um resumo de um livro de administração famoso, mas focado apenas nas
lições práticas para iniciantes.

**Tarefa Extra:** Tente "quebrar" a IA. Faça um prompt confuso e veja como ela
reage. Depois, conserte-o usando as técnicas aprendidas.

### Guia para o Professor

- **Instruções Didáticas:** Desafie os alunos a conseguirem a resposta perfeita
  na **primeira tentativa**. Avalie os prompts deles, não apenas as respostas da
  IA.
- **Perguntas para a Turma:**
  - "Qual parte da estrutura (Persona, Contexto, etc.) fez mais diferença no seu
    resultado?"
  - "A IA seguiu todas as suas restrições (ex: número de palavras)?"
- **Dicas de Condução:** Circule e peça para os alunos lerem seus prompts em voz
  alta para a turma comparar.

### Entrega

- Registrar a atividade no [Formulário da Aula 37](formulario-aula-37).
- Anexar ou informar o link do arquivo, pasta, apresentação ou evidência
  produzida.
- Manter o portfólio organizado com nome de arquivo coerente e data da aula.---

## 4. Estrutura do Formulário (Google Forms)

| Ordem | Pergunta                                                       | Tipo de Resposta | Observação                                         |
| :---: | :------------------------------------------------------------- | :--------------- | :------------------------------------------------- |
|   1   | Nome Completo                                                  | Resposta curta   | Obrigatório                                        |
|   2   | O que é uma 'Persona' em um prompt?                            | Múltipla escolha | Definir um papel ou cargo para a IA assumir        |
|   3   | Por que usar o framework Persona-Contexto-Tarefa-Formato?      | Múltipla escolha | Para dar clareza e aumentar a precisão da resposta |
|   4   | Escreva abaixo o melhor prompt que você criou na aula de hoje. | Resposta longa   | Evidência de prática                               |

---

## 5. Dicas de Ouro para o Professor

1. **Iteração:** Lembre que o Prompt Engineering é um processo de tentativa e
   erro. "Se não ficou bom, mude o prompt, não desista da IA".
2. **Idioma:** Mencione que, às vezes, prompts em inglês (mesmo traduzidos pelo
   tradutor) podem gerar resultados melhores em modelos globais, embora o
   português esteja excelente.
3. **Variáveis:** Ensine a usar colchetes `[ ]` para indicar onde o usuário deve
   preencher informações (ex: "Olá [NOME_DO_CLIENTE]").

---

## 6. Anexos e Referências

- **Materiais:**
  [Cheat Sheet de Prompt Engineering](/self/courses/2026-PTIC-Projetos-TIC-Tecnico-Administracao/materiais/material-20)
  [Atividade 37 - Prompt Engineering](/self/courses/2026-PTIC-Projetos-TIC-Tecnico-Administracao/atividades/atividade-37)
- **Links Úteis:**
  [Curso Rápido de Engenharia de Prompts](https://www.youtube.com/watch?v=_ZvnD737IsU)

---

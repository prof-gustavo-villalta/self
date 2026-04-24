---
layout: aula
title: "Aula 07 - Síntese do 1º Bimestre + Recuperação + Portfólio"
course_id: mobile2
category: aulas
---

## Data e contexto

- **Data:** 29/04/2026
- **Duração:** 5 horas-aula (250 min)
- **Horário:** 18h45 às 23h10 (considerando 15 min de intervalo)
- **Laboratório:** 6

## Alinhamento com o PTD

- **Habilidades:** 1.1 a 1.5 (Sintese)
- **Bases:** Revisão prática; ajustes de projeto; orientação individual para
  recuperação contínua; consolidação de portfólio.

---

## 1. Diagnóstico de Competências e Nivelamento (50 min)

### Conteúdo:

- Revisão dos pilares do bimestre: Setup, Dart, Widgets, Listas, Forms e Auth.
- Identificação de "Gaps" individuais e coletivos.
- Organização das trilhas de trabalho para a aula.

### Guia para o Professor:

- **Condução Técnica:** Faça uma enquete rápida (mão levantada) sobre quem
  concluiu cada atividade (1 a 4). Divida a sala em grupos: quem já terminou
  tudo (Trilha Avançada) e quem tem pendências (Trilha de Recuperação).
- **Debugging:** Ajude os alunos da Trilha de Recuperação a identificarem se o
  problema é de ambiente (setup) ou de lógica (Dart/Flutter).
- **Boas Práticas:** Incentive os alunos avançados a atuarem como "mentores" dos
  colegas, reforçando o aprendizado por meio da explicação.

---

## 2. Oficina de Refatoração e "Clean Code" (50 min)

### Conteúdo:

- Organização de pastas (`models`, `screens`, `widgets`, `services`).
- Padronização de nomes de classes e variáveis (CamelCase).
- Remoção de códigos comentados e avisos do Linter (Azul/Amarelo).

### Guia para o Professor:

- **Condução Técnica:** Mostre como o VS Code ajuda a mover arquivos e atualizar
  os imports automaticamente. Explique por que não devemos ignorar os "blue
  lines" do linter (ex: usar `const` onde for possível).
- **Debugging:** Se ao mover um arquivo o app parar de compilar, ensine o atalho
  `Ctrl + .` para corrigir o import automaticamente no VS Code.
- **Boas Práticas:** Um código limpo é mais fácil de dar manutenção. Use o
  comando `flutter format .` para auto-identar o projeto inteiro.

---

## 3. Consolidação do Portfólio de Evidências (50 min)

### Conteúdo:

- Estrutura do README do projeto.
- Registro de Prints/Vídeos do app funcionando.
- Organização do repositório no GitHub ou pasta no Google Drive.

### Guia para o Professor:

- **Condução Técnica:** O portfólio é a prova do aprendizado. Ajude os alunos a
  escreverem um README simples: Título, Descrição, Tecnologias Usadas e um Print
  do app.
- **Debugging:** Se o aluno perdeu o código por falha no PC do lab, ajude-o a
  recuperar a última versão enviada ou a reconstruir a parte essencial com base
  nos exemplos da aula.
- **Boas Práticas:** Use o `.gitignore` padrão do Flutter para não subir a pasta
  `build/`, que é pesada e desnecessária no repositório.

---

## 4. Plantão de Dúvidas e Recuperação Ativa (50 min)

### Conteúdo:

- Atendimento individualizado para destravar projetos.
- Reentrega orientada de atividades pendentes.
- Desafio de bônus para alunos adiantados (ex: tema escuro/claro).

### Guia para o Professor:

- **Condução Técnica:** Foque nos alunos que ainda não conseguiram o "Hello
  World" ou que estão travados na navegação entre telas. Garanta que todos
  tenham pelo menos uma atividade funcional.
- **Debugging:** Erros de "Overflow" são comuns em layouts de alunos. Mostre
  como usar o `Expanded` ou `SingleChildScrollView` para resolver de vez.
- **Boas Práticas:** Documente quem realizou a recuperação para controle do PTD
  e conselho de classe.

---

## 5. Fechamento e Planejamento do 2º Bimestre (50 min)

### Conteúdo:

- Checkpoint final de notas/menções intermediárias.
- Introdução ao tema do próximo bimestre: APIs Reais e Recursos Nativos.
- Autoavaliação do progresso técnico.

### Guia para o Professor:

- **Condução Técnica:** Apresente o que vem por aí: Consumo de APIs REST (JSON),
  Câmera, GPS e Mapas. Isso gera expectativa e motivação para a próxima etapa.
- **Debugging:** Verifique se algum aluno ainda tem problemas de setup que podem
  impedir o uso de APIs na próxima aula (ex: bloqueios de rede no emulador).
- **Encerramento:** Peça para os alunos preencherem o formulário de
  autoavaliação e confirmarem a entrega do link do portfólio.

---

## Estrutura do Formulário (Google Forms)

| Ordem | Pergunta                                                           | Tipo de Resposta | Observação Técnica                               |
| :---- | :----------------------------------------------------------------- | :--------------- | :----------------------------------------------- |
| 1     | Nome Completo                                                      | Resposta curta   | Identificação                                    |
| 2     | Qual o status atual das suas atividades (1 a 4)?                   | Múltipla Escolha | [Todas concluídas / Algumas pendentes / Nenhuma] |
| 3     | Qual conceito do 1º bimestre foi o mais difícil para você?         | Parágrafo        | Diagnóstico pedagógico                           |
| 4     | O seu código segue a organização de pastas (models, screens, etc)? | Múltipla Escolha | Avalia organização                               |
| 5     | Link atualizado do seu Portfólio (GitHub/Drive)                    | Texto curto      | Coleta de evidência final                        |

---

## Dicas de Ouro para o Professor (Lab Noturno)

1. **Clima de Conselho:** No final do bimestre, os alunos ficam ansiosos com
   notas. Mantenha um clima de transparência e parceria. Mostre que a
   "recuperação" é uma oportunidade de aprendizado, não uma punição.
2. **Backups Externos:** Em labs de escola, arquivos podem sumir após
   reinicializações. Insista para que os alunos usem pendrives ou nuvem
   (GitHub/Drive) antes de saírem. Nunca confie no "Desktop" do PC da escola.
3. **Energia Final:** Sendo a última aula do bimestre, muitos alunos podem
   faltar ou querer sair cedo. Reserve o Bloco 5 para uma "Demo" rápida dos apps
   mais legais da sala para manter todos até o fim e valorizar o trabalho.

## Materiais Relacionados

- [Material 01 - Setup Padrão](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-01)
- [Atividade 07 - Checkpoint de Portfólio](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-07)

---

**Material elaborado para o curso de PAM2 - 2026**  
Prof. Gustavo Villalta

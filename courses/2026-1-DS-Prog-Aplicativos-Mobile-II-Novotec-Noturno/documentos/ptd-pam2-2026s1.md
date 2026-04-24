---
layout: page
title: "PTD 2026 - Mobile II"
---

# Plano de Trabalho Docente (PTD) 2026

**Componente curricular: Programação de Aplicativos Mobile II (PDAM2)**

| Informação                | Detalhe                                      |
| :------------------------ | :------------------------------------------- |
| **ETEC**                  | Ferrucio Humberto Gazzetta -- Nova Odessa    |
| **Curso / Habilitação**   | Técnico em Desenvolvimento de Sistemas       |
| **Componente Curricular** | Programação de Aplicativos Mobile II (PDAM2) |
| **Natureza do Curso**     | Semestral                                    |
| **Dia das Aulas**         | Quartas-feiras                               |
| **Período Considerado**   | 18/03/2026 a 06/07/2026                      |
| **Professor(a)**          | Prof. Gustavo Villalta                       |
| **Módulo / Turma**        | 2º Módulo / Noturno                          |
| **Carga Horária Semanal** | 5 aulas semanais                             |

**Observação técnica:** como 17/03/2026 caiu em uma terça-feira, o cronograma
abaixo foi organizado a partir da primeira quarta-feira letiva subsequente,
18/03/2026, mantendo o encerramento do 1º semestre em 06/07/2026, conforme o
calendário escolar.

# I -- Atribuições e Atividades Profissionais

- Documentar, construir e manter sistemas de informação para plataformas móveis.
- Desenvolver aplicações para dispositivos móveis com integração a serviços,
  bancos de dados e recursos nativos do aparelho.
- Selecionar ambientes, bibliotecas e estratégias de empacotamento e
  distribuição adequadas ao desenvolvimento mobile.

# II -- Competências, Habilidades, Valores e Bases Tecnológicas

## Competência

1. Projetar aplicativos, selecionando linguagens de programação e ambientes de
   desenvolvimento.

## Habilidades

- 1.1 Codificar aplicativos em tecnologia móvel.
- 1.2 Utilizar ambientes de desenvolvimento mobile.
- 1.3 Elaborar aplicativos com acesso a banco de dados.
- 1.4 Construir layout de aplicativos para dispositivos móveis.
- 1.5 Utilizar recursos avançados do dispositivo (smartphones e tablets).

## Valores e Atitudes

- Incentivar a criatividade.
- Estimular a organização.
- Responsabilizar-se pela produção, utilização e divulgação de informações.

## Bases Tecnológicas

- **Plataforma e linguagem**: Flutter e Dart; estrutura de projeto; organização
  em camadas.
- **Interface e navegação**: Widgets, layout responsivo, temas; navegação e
  rotas.
- **Gerência de estado**: padrões e bibliotecas (ex.: Provider/Riverpod/BLoC),
  conforme o projeto.
- **Conectividade**: consumo de APIs REST; comunicação em tempo real
  (WebSocket/sockets) quando aplicável.
- **Persistência**: armazenamento local e sincronização com serviços (quando
  aplicável).
- **Autenticação e autorização**: tokens, sessões, segurança básica e boas
  práticas.
- **Recursos do dispositivo**: câmera, sensores, localização, orientação e mapas
  (via plugins).
- **Empacotamento e distribuição**: build, assinatura, publicação e checklist de
  entrega.
- **Qualidade**: testes (unit/widget), tratamento de erros, logs e
  observabilidade básica.

# III -- Procedimento Didático e Cronograma de Desenvolvimento

## Metodologias e organização das aulas (Flutter)

- **Aprendizagem baseada em projeto (PjBL)**: um projeto semestral evolui em
  incrementos (sprints curtas), com entregas parciais demonstráveis.
- **Aprendizagem baseada em problemas (PBL)**: cada tópico parte de um problema
  real (offline/online, erros de rede, permissões, desempenho), resolvido com
  orientação e pesquisa guiada.
- **Sala de aula invertida (microconteúdo)**: preparação prévia curta
  (leitura/vídeo) para liberar tempo de laboratório e debugging em aula.
- **Prática colaborativa**: programação em pares (pair programming), revisão
  entre pares (code review) e discussão de decisões técnicas.
- **Portfólio e evidências**: registro contínuo (commits, checklist, relatórios
  curtos) para consolidar autonomia e rastreabilidade.

### Rotina semanal (4 aulas)

- **Aula 1**: objetivos, revisão e aquecimento (mini-desafio).
- **Aula 2**: demonstração guiada + prática assistida.
- **Aula 3**: desenvolvimento em sprint (pares/grupos) com acompanhamento.
- **Aula 4**: code review, testes/checklist, devolutiva e planejamento do
  próximo incremento.

| Período / Aulas | Habilidades   | Bases Tecnológicas                                                                                                                                                   | Procedimentos Didáticos                                                                                                                                                          | Observações / Datas                                                                           |
| :-------------- | :------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------- |
| 18/03 e 25/03   | 1.1, 1.2      | Apresentação do componente; visão geral do desenvolvimento mobile; configuração do ambiente Flutter; estrutura do projeto; organização do fluxo de trabalho.         | Aulas expositivas dialogadas, demonstração guiada, setup do ambiente, prática assistida em laboratório e exercício de criação do primeiro app (Hello/Counter) com versionamento. | Início efetivo em quarta-feira após 17/03.                                                    |
| 01/04 e 08/04   | 1.1, 1.4      | Construção de interfaces (Widgets); layout responsivo; navegação entre telas; usabilidade básica.                                                                    | Laboratório orientado com prototipação, implementação incremental e devolutiva por checklist; mini-sprint com entrega de telas navegáveis.                                       | 09/04: PTDs publicados à comunidade escolar.                                                  |
| 15/04 e 22/04   | 1.1, 1.3, 1.4 | Formulários e validação; autenticação (conceitos e implementação); persistência inicial (local e/ou remota).                                                         | Estudo de caso, codificação em pares, implementação por etapas e revisão entre pares (PR/checklist) com mediação docente.                                                        | 22 a 27/04: entrega de resultados intermediários do 1º bimestre.                              |
| 29/04           | 1.1 a 1.5     | Síntese dos conteúdos do bimestre, ajustes de projeto e orientação individual para recuperação contínua.                                                             | Plantão de dúvidas, revisão prática, acompanhamento individual e consolidação de portfólio.                                                                                      | 29 e 30/04: Conselho de Classe Intermediário.                                                 |
| 06/05 e 13/05   | 1.1, 1.3, 1.5 | Consumo de APIs REST; HTTP (GET/POST); serialização JSON; tratamento de erros e estados de carregamento.                                                             | Aulas práticas com leitura de documentação, laboratório com API e atividade formativa com rubrica (funcionalidade + qualidade).                                                  | 12/05: 2ª reunião de pais.                                                                    |
| 20/05 e 27/05   | 1.1, 1.5      | Recursos do dispositivo via plugins: câmera, sensores e permissões; ciclo de vida; exceções e logs.                                                                  | Demonstração técnica, laboratório orientado, checklist de permissões e implementação com validação em dispositivo/emulador.                                                      | 20/05: reunião do Conselho de Escola.                                                         |
| 03/06 e 10/06   | 1.1, 1.5      | Localização e mapas; geolocalização; exibição de mapas e contexto geográfico na aplicação.                                                                           | Resolução de problemas em laboratório, validação por rubrica e revisão entre pares do incremento entregue.                                                                       | 04 e 05/06 não letivos; 13/06 sábado letivo referente a 05/06.                                |
| 17/06 e 24/06   | 1.1 a 1.5     | Conectividade avançada (WebSocket/sockets) e integração (quando aplicável); Bluetooth e/ou dispositivos embarcados (quando aplicável); refinamento do projeto final. | Projeto orientado em sprint, code review, refatoração guiada e acompanhamento de entregas com foco em qualidade.                                                                 | 23 e 24/06: apresentação de TCC da escola; 22 a 26/06: renovação de matrícula.                |
| 01/07           | 1.1 a 1.5     | Empacotamento, testes, preparação para distribuição, apresentação final e fechamento do componente.                                                                  | Demonstração do produto, avaliação por rubrica, autoavaliação, devolutiva docente e fechamento do portfólio.                                                                     | 06/07: fim das aulas do 1º semestre; 01 a 06/07: entrega de resultados finais do 2º bimestre. |

# IV -- Plano de Avaliação de Competências

| Competência                                                                                  | Instrumentos e Procedimentos                                                                                                                                                                                                  | Critérios de Desempenho                                                                                                                                                                                                                                        | Evidências de Desempenho                                                                                                                                                                                                                          |
| :------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Projetar aplicativos, selecionando linguagens de programação e ambientes de desenvolvimento. | Avaliação prática em laboratório; exercícios orientados; portfólio de atividades; mini-projetos; projeto semestral incremental (sprints); apresentações (demos) e entregas parciais com rubrica; participação em code review. | Execução funcional do produto; organização do código (estrutura Flutter); uso adequado do ambiente; aplicação correta de interfaces, dados, APIs e recursos do dispositivo; tratamento de erros e estados; cumprimento de prazos; autonomia e clareza técnica. | O estudante desenvolve aplicação Flutter funcional, integra serviços e/ou dados, utiliza recursos do dispositivo quando pertinente, registra evidências do processo (portfólio/commits) e apresenta solução coerente com os requisitos propostos. |

# V -- Estratégias de Recuperação Contínua

- Retomada guiada dos conteúdos com maior índice de dificuldade.
- Listas de exercícios, estudos de caso e atividades práticas em laboratório.
- Atendimento individual e orientação por etapas do projeto.
- Reentrega orientada de atividades, com feedback específico sobre correções
  necessárias.

---

[Voltar para Referências](../referencias/)

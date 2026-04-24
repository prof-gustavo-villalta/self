---
layout: aula
title: "Aula 11 - Sensores do Dispositivo + Ciclo de Vida"
course_id: mobile2
category: aulas
---

## Data e contexto

- **Duração**: 5 horas-aula (250 minutos)
- **Laboratório**: 6 (Ambiente ETEC Noturno)
- **Pré-requisito**: Aula 10 (Permissões)

## Alinhamento com o PTD

- **Habilidades**: 1.1 Codificar aplicativos em tecnologia móvel; 1.5 Utilizar
  recursos avançados do dispositivo.
- **Bases**: sensores; eventos do ciclo de vida; tratamento de erros.

## Objetivos da aula (Professor)

- Manipular streams de dados vindos do Acelerômetro e Giroscópio.
- Ensinar a gerenciar o Ciclo de Vida do App para evitar consumo excessivo de
  bateria (Memory Leaks).
- Criar uma interface reativa que responde ao movimento físico do aparelho.

## Roteiro por blocos (5 x 50 min)

### Bloco 1 (50 min): Introdução aos Sensores e Streams

- **Teoria**: O que é um Stream em Flutter? (Analogia da torneira aberta).
- **Prática**: Instalação do pacote `sensors_plus`.
- **Demonstração**: Exibição bruta dos valores X, Y e Z no console.

### Bloco 2 (50 min): UI Reativa com StreamBuilder

- **Conceito**: Por que usar `StreamBuilder` em vez de `setState` para sensores?
- **Prática**: Criar um Widget que muda de cor ou posição conforme a inclinação
  do celular.
- **UX**: Arredondamento de casas decimais para evitar "tremulação" visual.

### Bloco 3 (50 min): Ciclo de Vida do App (WidgetsBindingObserver)

- **Teoria**: Estados `resumed`, `inactive` e `paused`.
- **Prática**: Implementar o `dispose()` corretamente para fechar o listener do
  sensor.
- **Teste**: O sensor continua rodando com o app em background? (Mostrar o
  perigo disso).

### Bloco 4 (50 min): Mini-Projeto: Nível de Bolha ou Pedômetro

- **Desafio**: Implementar a lógica de um "Nível" (centralizar um ícone na
  tela).
- **Lógica**: Uso de `math` para calcular ângulos ou limiares de movimento
  (Shake detection).
- **Refinamento**: Adicionar feedback tátil (vibration) ao atingir um objetivo.

### Bloco 5 (50 min): Laboratório e Publicação

- **Atividade**: Finalizar o mini-desafio e testar em movimento real.
- **Evidência**: Vídeo curto do app reagindo ao movimento ou print da tela de
  "nível".
- **Fechamento**: Sincronização de código e preenchimento do formulário.

## Guia para o Professor

- **Atenção**: Emuladores têm suporte limitado a sensores. Use o "Virtual
  Sensors" do Android Studio, mas priorize o **celular real**.
- **Matemática**: Alguns alunos podem travar no cálculo de X/Y. Tenha um snippet
  pronto para normalizar os valores entre 0 e 1.
- **Performance**: Explique que atualizar a tela 60 vezes por segundo com dados
  do sensor exige cuidado com a complexidade do Widget.

## Estrutura do Formulário Google

1. **Nome Completo**
2. **Link do Repositório (GitHub)**
3. **Pergunta Técnica**: Por que é vital cancelar a assinatura (subscription) de
   um sensor no método `dispose()`?
4. **Desafio**: Qual sensor você usou (Acelerômetro ou Giroscópio) e qual foi o
   maior valor registrado em um movimento brusco?

## Dicas de Ouro (ETEC Noturno)

1. **Evite Emuladores Pesados**: No lab da ETEC, abrir o emulador e o VS Code ao
   mesmo tempo pode congelar a máquina. Celular físico é a salvação.
2. **Cuidado com o Barulho**: Se usar sensores para disparar sons (ex: alarme de
   movimento), peça para os alunos usarem fones ou volume baixo para não virar
   bagunça.
3. **Git no Início**: Como o tempo é curto, peça para darem o primeiro
   `git push` logo no Bloco 1 para garantir que não percam nada se a energia
   oscilar.

## Registro e Coleta da Aula

- Atividade associada:
  [Atividade 11 - Sensores + UI Reativa](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-11)
- Formulário:
  [Formulário Aula 11](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-11)

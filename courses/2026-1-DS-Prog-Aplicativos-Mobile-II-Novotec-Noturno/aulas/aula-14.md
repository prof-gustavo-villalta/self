---
layout: aula
title: "Aula 14 - Tempo Real com WebSockets + Projeto Final"
course_id: mobile2
category: aulas
---

## Data e contexto

- **Duração**: 5 horas-aula (250 minutos)
- **Laboratório**: 6 (Ambiente ETEC Noturno)
- **Pré-requisito**: Aulas de HTTP e API REST

## Alinhamento com o PTD

- **Habilidades**: 1.1 Codificar aplicativos em tecnologia móvel; 1.3 Elaborar
  aplicativos com acesso a banco de dados.
- **Bases**: conectividade avançada; sockets; refinamento do projeto final.

## Objetivos da aula (Professor)

- Compreender a diferença entre requisições Stateless (HTTP) e conexões
  Full-Duplex (WebSockets).
- Implementar um cliente WebSocket para comunicação em tempo real
  (Chat/Notificações).
- Definir grupos e escopo técnico do Projeto Final do semestre.

## Roteiro por blocos (5 x 50 min)

### Bloco 1 (50 min): HTTP vs WebSockets

- **Teoria**: O problema do Polling e a solução dos Sockets.
- **Analogia**: Carta (HTTP) vs Ligação Telefônica (Socket).
- **Protocolo**: O handshake e a URL `ws://` ou `wss://`.

### Bloco 2 (50 min): Implementando um Cliente de Eco

- **Prática**: Uso do pacote `web_socket_channel`.
- **Implementação**: Conectar ao servidor `wss://echo.websocket.events`.
- **Fluxo**: Enviar uma mensagem e ouvir o retorno imediato via Stream.

### Bloco 3 (50 min): Chat em Tempo Real (UI)

- **Construção**: Criar uma interface de mensagens com `ListView.builder`.
- **Reatividade**: Integrar o `StreamBuilder` com o canal do WebSocket.
- **Desafio**: Lidar com a desconexão e tentar reconectar automaticamente.

### Bloco 4 (50 min): Definição do Projeto Final

- **Atividade**: Formação de grupos (máx 3 pessoas).
- **Escopo**: O app deve ter: Consumo de API, Recurso Nativo (Câmera/GPS) e
  Persistência.
- **Entrega**: Preenchimento do formulário de proposta de projeto.

### Bloco 5 (50 min): Sprint 0 - Setup do Projeto

- **Laboratório**: Criação do repositório oficial do grupo.
- **Organização**: Divisão de tarefas (Quem faz o quê).
- **Fechamento**: O professor valida as propostas de projeto e dá o "OK"
  técnico.

## Guia para o Professor

- **Servidor**: Tenha um servidor de WebSocket simples em Node.js ou use
  serviços públicos para evitar que a aula pare se o servidor cair.
- **Streams**: Reforce o conceito de que o WebSocket não "termina" a função após
  o envio; ele fica "escutando" até ser fechado.
- **Escopo**: Seja rigoroso na definição do projeto final. Impeça projetos
  mirabolantes que não serão terminados em 3 semanas.

## Estrutura do Formulário Google

1. **Nome Completo e Integrantes do Grupo**
2. **Título do Projeto Final**
3. **Resumo**: O que o app faz e qual problema resolve?
4. **Recursos Técnicos**: Quais recursos nativos e APIs serão utilizados?

## Dicas de Ouro (ETEC Noturno)

1. **Filtro de Conteúdo**: O firewall da ETEC pode bloquear portas de Sockets
   não convencionais. Teste a conexão na porta 80 ou 443.
2. **Mobile First**: Como o WebSocket depende muito da estabilidade da rede,
   ensine os alunos a verificarem o status da conexão (`connectivity_plus`)
   antes de tentar enviar dados.
3. **Simplicidade**: Para o projeto final, sugira temas como "Achei na ETEC"
   (GPS), "Inventário de TI" (Câmera/QR Code) ou "Chat da Sala" (WebSocket).

## Registro e Coleta da Aula

- Atividade associada:
  [Atividade 14 - WebSockets e Proposta de Projeto](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-14)
- Formulário:
  [Formulário Aula 14](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-14)

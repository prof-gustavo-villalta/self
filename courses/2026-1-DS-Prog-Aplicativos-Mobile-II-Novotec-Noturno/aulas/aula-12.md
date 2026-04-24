---
layout: aula
title: "Aula 12 - Localização (GPS) e Permissões de Local"
course_id: mobile2
category: aulas
---

## Data e contexto

- **Duração**: 5 horas-aula (250 minutos)
- **Laboratório**: 6 (Ambiente ETEC Noturno)
- **Pré-requisito**: Aula 10 (Conceitos de Permissões)

## Alinhamento com o PTD

- **Habilidades**: 1.1 Codificar aplicativos em tecnologia móvel; 1.5 Utilizar
  recursos avançados do dispositivo.
- **Bases**: localização; GPS; permissões; tratamento de erros.

## Objetivos da aula (Professor)

- Obter as coordenadas geográficas (Latitude e Longitude) do dispositivo.
- Diferenciar permissão "Durante o uso" de "Sempre" e "Localização Aproximada"
  de "Precisa".
- Implementar o acompanhamento de posição em tempo real (Tracking).

## Roteiro por blocos (5 x 50 min)

### Bloco 1 (50 min): Setup de Localização e Geolocator

- **Teoria**: Como o GPS funciona (Satélites vs Torres vs Wi-Fi).
- **Prática**: Configuração do pacote `geolocator`.
- **Configuração**: Alterar `AndroidManifest.xml` (ACCESS_FINE_LOCATION) e
  `Info.plist`.

### Bloco 2 (50 min): O Fluxo de Permissão Robusto

- **Lógica**: Verificar se o serviço de GPS está ligado -> Verificar permissão
  -> Solicitar permissão.
- **Prática**: Criar uma função `_determinarPosicao()` que lida com todos os
  casos de erro.
- **UX**: Mostrar diálogos explicativos antes de pedir a permissão do sistema.

### Bloco 3 (50 min): Captura da Posição Atual

- **Implementação**: Uso de `Geolocator.getCurrentPosition()`.
- **Desafio**: Converter coordenadas em endereço legível (Geocoding reverso)
  usando o pacote `geocoding`.
- **Feedback**: Exibir um mapa estático ou link para o Google Maps com as
  coordenadas.

### Bloco 4 (50 min): Tracking em Tempo Real

- **Implementação**: Uso de `Geolocator.getPositionStream()`.
- **Cenário**: Atualizar a distância percorrida entre o ponto A e o ponto B.
- **Otimização**: Configurar a distância mínima (distanceFilter) para evitar
  atualizações desnecessárias.

### Bloco 5 (50 min): Laboratório e Testes de Campo

- **Atividade**: Criar um app que mostra "Onde estou agora?".
- **Teste**: Sair do laboratório para o pátio (se permitido) para ver a variação
  do GPS.
- **Fechamento**: Discussão sobre privacidade e coleta de dados de localização.

## Guia para o Professor

- **Dica de Emulador**: Ensine os alunos a usarem os "Extended Controls" do
  Android Emulator para simular rotas e pontos GPS fixos.
- **Erro Comum**: Se o GPS estiver desligado no sistema, o app lançará uma
  exceção. O aluno **deve** tratar isso.
- **Bateria**: Explique que o GPS é um dos maiores vilões da bateria e deve ser
  desligado quando não for essencial.

## Estrutura do Formulário Google

1. **Nome Completo**
2. **Link do Repositório (GitHub)**
3. **Pergunta Técnica**: Qual a diferença entre `ACCESS_COARSE_LOCATION` e
   `ACCESS_FINE_LOCATION`?
4. **Desafio**: Cole as coordenadas (Lat/Long) capturadas pelo seu app no pátio
   ou na sala.

## Dicas de Ouro (ETEC Noturno)

1. **Sinal de GPS Interno**: Dentro do lab da ETEC, o sinal de GPS real é fraco.
   Use a ferramenta de "Simulation" do emulador para garantir que o código
   funciona.
2. **Wi-Fi da Escola**: O GPS do Android usa o Wi-Fi para melhorar a precisão
   (A-GPS). Certifique-se de que os alunos estão conectados à rede da escola.
3. **Offline Geocoding**: O pacote `geocoding` precisa de internet para buscar
   endereços. Se a rede oscilar, o app pode travar na busca do endereço. Use
   `try-catch`.

## Registro e Coleta da Aula

- Atividade associada:
  [Atividade 12 - GPS e Localização](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-12)
- Formulário:
  [Formulário Aula 12](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-12)

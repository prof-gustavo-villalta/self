---
layout: aula
title: "Aula 13 - Mapas (Google Maps) + Marcadores"
course_id: mobile2
category: aulas
---

## Data e contexto

- **Duração**: 5 horas-aula (250 minutos)
- **Laboratório**: 6 (Ambiente ETEC Noturno)
- **Pré-requisito**: Aula 12 (Coordenadas GPS)

## Alinhamento com o PTD

- **Habilidades**: 1.1 Codificar aplicativos em tecnologia móvel; 1.5 Utilizar
  recursos avançados do dispositivo.
- **Bases**: mapas; contexto geográfico; integração de serviços.

## Objetivos da aula (Professor)

- Integrar o SDK do Google Maps no Flutter.
- Exibir mapas interativos com controle de câmera e zoom.
- Manipular Marcadores (Markers) dinâmicos baseados na posição do usuário.

## Roteiro por blocos (5 x 50 min)

### Bloco 1 (50 min): Google Cloud e API Key

- **Configuração**: Criar projeto no Google Cloud Console e habilitar o "Maps
  SDK for Android".
- **Segurança**: Como restringir a API Key (Teoria) e onde colá-la no projeto
  Flutter.
- **Dependência**: Instalação do pacote `google_maps_flutter`.

### Bloco 2 (50 min): Exibindo o Mapa Base

- **Implementação**: O Widget `GoogleMap`.
- **Propriedades**: `initialCameraPosition`, `mapType` (Normal, Satélite,
  Híbrido).
- **Tratamento**: Lidar com o carregamento assíncrono do controlador do mapa.

### Bloco 3 (50 min): Marcadores e Janelas de Informação

- **Prática**: Adicionar um marcador fixo na localização da ETEC.
- **Interação**: Adicionar um marcador ao clicar longamente no mapa
  (onLongPress).
- **Customização**: Mudar a cor do ícone do marcador e adicionar `infoWindow`.

### Bloco 4 (50 min): Integrando GPS com Mapas

- **Lógica**: Obter a posição atual (Aula 12) e mover a câmera do mapa
  automaticamente.
- **Implementação**: `GoogleMapController.animateCamera`.
- **UX**: Botão "Minha Localização" nativo do Google Maps.

### Bloco 5 (50 min): Laboratório: App de Check-in Geográfico

- **Atividade**: O aluno deve criar um mapa onde ele clica e "salva" um marcador
  com um título.
- **Desafio**: Manter o estado dos marcadores em uma lista durante a execução.
- **Fechamento**: Demonstração dos mapas funcionando e sincronização com o Git.

## Guia para o Professor

- **API Keys**: O Google exige cartão de crédito para ativar o faturamento, mas
  o plano gratuito é generoso. Para a aula, o professor pode fornecer uma key de
  teste ou usar o simulador de mapas.
- **Versão do Android**: O Google Maps exige uma versão mínima do SDK do Android
  (geralmente 21+). Verifique o `build.gradle`.
- **Build**: O primeiro build com mapas demora bastante. Peça aos alunos para
  rodarem o app logo após adicionar a dependência.

## Estrutura do Formulário Google

1. **Nome Completo**
2. **Link do Repositório (GitHub)**
3. **Pergunta Técnica**: Qual a função do objeto `GoogleMapController`?
4. **Desafio**: Envie um print do mapa do seu app centralizado na escola com um
   marcador escrito "Estou aqui!".

## Dicas de Ouro (ETEC Noturno)

1. **Proxy do Laboratório**: Se o mapa ficar com a tela cinza e apenas o logo do
   Google, pode ser bloqueio de firewall ou API Key inválida. Verifique o
   Logcat.
2. **Key Compartilhada**: Se os alunos não conseguirem criar suas próprias Keys
   no Google Cloud, tenha uma Key "da sala" preparada apenas para esta aula (com
   restrição de pacote).
3. **Limpeza de Build**: Se der erro de "Native method not found", execute
   `flutter clean` e `flutter run`.

## Registro e Coleta da Aula

- Atividade associada:
  [Atividade 13 - Mapas e Marcadores](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-13)
- Formulário:
  [Formulário Aula 13](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-13)

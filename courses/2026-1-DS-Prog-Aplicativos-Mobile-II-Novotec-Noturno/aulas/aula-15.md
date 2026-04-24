---
layout: aula
title: "Aula 15 - Bluetooth e Comunicação com Dispositivos"
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
- **Bases**: conectividade avançada; Bluetooth; integração com dispositivos.

## Objetivos da aula (Professor)

- Entender as diferenças entre Bluetooth Classic e Bluetooth Low Energy (BLE).
- Implementar a varredura (Scan) e conexão com dispositivos próximos.
- Realizar a leitura e escrita de dados via Bluetooth.

## Roteiro por blocos (5 x 50 min)

### Bloco 1 (50 min): Conceitos de Bluetooth e BLE

- **Teoria**: O que é BLE? (GATT, Services, Characteristics).
- **Prática**: Permissões críticas no Android 12+ (BLUETOOTH_SCAN,
  BLUETOOTH_CONNECT, Location).
- **Dependência**: Instalação do pacote `flutter_blue_plus`.

### Bloco 2 (50 min): Escaneando Dispositivos

- **Implementação**: Iniciar o scan e exibir a lista de dispositivos
  encontrados.
- **UI**: Lista com nome, ID (MAC Address) e força do sinal (RSSI).
- **Filtro**: Filtrar apenas dispositivos com nomes específicos (ex: "ESP32" ou
  "Arduino").

### Bloco 3 (50 min): Conexão e Descoberta de Serviços

- **Lógica**: Clicar no item da lista e estabelecer a conexão.
- **Exploração**: Descobrir quais serviços o dispositivo oferece.
- **Segurança**: Lidar com falhas de pareamento e desconexões inesperadas.

### Bloco 4 (50 min): Troca de Dados (Read/Write)

- **Prática**: Enviar um comando (ex: "Ligar LED") e ler um status (ex:
  "Temperatura: 25ºC").
- **Monitoramento**: Uso de Notificações/Indicações para receber dados sem
  precisar pedir (Push).
- **Mocks**: Se não houver hardware, usar apps de "Bluetooth Simulator" no
  celular.

### Bloco 5 (50 min): Sprint do Projeto Final

- **Laboratório**: Desenvolvimento focado no Projeto Final.
- **Acompanhamento**: Professor passa em cada grupo resolvendo travamentos
  técnicos.
- **Fechamento**: Planejamento da aula de encerramento e apresentações.

## Guia para o Professor

- **Hardware**: Esta aula é desafiadora sem hardware real. Se possível, tenha 2
  ou 3 ESP32 ou Arduinos configurados.
- **Alternativa**: Alunos podem usar um segundo celular com o app "nRF Connect"
  para simular um periférico BLE.
- **Permissões**: No Android moderno, o Bluetooth requer localização ativada
  para fazer o Scan. Explique essa "curiosidade" aos alunos.

## Estrutura do Formulário Google

1. **Nome Completo**
2. **Link do Repositório (GitHub)**
3. **Pergunta Técnica**: O que é uma "Characteristic" no protocolo Bluetooth
   BLE?
4. **Status do Projeto**: O que o grupo conseguiu implementar do projeto final
   até agora?

## Dicas de Ouro (ETEC Noturno)

1. **Bluetooth nos PCs**: Os desktops da ETEC raramente têm Bluetooth. Os testes
   **precisam** ser feitos em dispositivos físicos reais.
2. **Poluição de Sinais**: Com 30 alunos escaneando ao mesmo tempo, a lista de
   dispositivos será enorme. Ensine a filtrar pelo nome do dispositivo para não
   se perderem.
3. **Bateria e Bluetooth**: Lembre os alunos de desligarem o Bluetooth após a
   aula para não drenarem a bateria dos seus celulares no trajeto de volta.

## Registro e Coleta da Aula

- Atividade associada:
  [Atividade 15 - Bluetooth e Sprint Final](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-15)
- Formulário:
  [Formulário Aula 15](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-15)

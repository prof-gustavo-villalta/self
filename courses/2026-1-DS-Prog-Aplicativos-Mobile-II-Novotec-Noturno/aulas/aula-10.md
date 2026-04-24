---
layout: aula
title: "Aula 10 - Recursos do Dispositivo: Câmera e Galeria + Permissões"
course_id: mobile2
category: aulas
---

## Data e contexto

- **Duração**: 5 horas-aula (250 minutos)
- **Laboratório**: 6 (Ambiente ETEC Noturno)
- **Pré-requisito**: Conhecimentos de UI básica e Gerenciamento de Estado

## Alinhamento com o PTD

- **Habilidades**: 1.1 Codificar aplicativos em tecnologia móvel; 1.5 Utilizar
  recursos avançados do dispositivo.
- **Bases**: recursos do dispositivo; câmera; permissões; tratamento de erros.

## Objetivos da aula (Professor)

- Implementar a captura de fotos e seleção de imagens da galeria.
- Ensinar o fluxo correto de solicitação e tratamento de permissões no
  Android/iOS.
- Garantir que o aluno saiba exibir um preview da imagem capturada na UI.

## Roteiro por blocos (5 x 50 min)

### Bloco 1 (50 min): Conceitos e Dependências

- **Teoria**: Diferença entre permissões de instalação e em tempo de execução.
- **Prática**: Adição do plugin `image_picker` e configuração do
  `AndroidManifest.xml` e `Info.plist`.
- **Destaque**: Por que o app quebra se não tratarmos a permissão negada?

### Bloco 2 (50 min): Galeria e UI de Preview

- **Implementação**: Criar um serviço para abrir a galeria.
- **UI**: Widget `Image.file` para exibir o arquivo selecionado.
- **Tratamento**: Caso o usuário abra a galeria mas não selecione nada (retorno
  nulo).

### Bloco 3 (50 min): Câmera e Captura Real

- **Implementação**: Trocar a fonte de `ImageSource.gallery` para
  `ImageSource.camera`.
- **Desafio**: Lidar com a rotação da imagem e o armazenamento temporário.
- **Feedback**: Exibir um `CircularProgressIndicator` enquanto a câmera é
  processada.

### Bloco 4 (50 min): Tratamento de Erros e UX

- **Cenários**: "E se o celular não tiver câmera?", "E se o armazenamento
  estiver cheio?".
- **Melhoria**: Uso de `SnackBar` para informar o status ao usuário de forma
  amigável.
- **Refatoração**: Organizar o código em um Controller ou Provider.

### Bloco 5 (50 min): Laboratório e Evidência

- **Atividade**: Finalizar o app com os dois botões (Câmera e Galeria).
- **Checklist**: O app exibe a foto? O app avisa se a permissão foi negada?
- **Fechamento**: Coleta de evidências e commit no GitHub.

## Guia para o Professor

- **Hardware**: O emulador do VS Code muitas vezes falha na câmera; incentive o
  uso de **dispositivo físico via USB**.
- **Dependência**: Verifique se o aluno adicionou as permissões no arquivo XML,
  caso contrário o app fechará sem erro claro no console.
- **Ponte**: Mencione que essa imagem poderá ser enviada para a API nas próximas
  aulas (Multipart request).

## Estrutura do Formulário Google

1. **Nome Completo**
2. **Link do Repositório/Pasta (GitHub/Drive)**
3. **Pergunta Técnica**: Qual a diferença entre os parâmetros
   `ImageSource.camera` e `ImageSource.gallery`?
4. **Desafio**: Descreva o que aconteceu no seu app quando você negou a
   permissão de câmera.

## Dicas de Ouro (ETEC Noturno)

1. **Cabo USB Próprio**: Muitos cabos do laboratório são apenas para carga. Peça
   aos alunos para trazerem seus próprios cabos de dados.
2. **Hot Reload vs Restart**: Mudanças no `AndroidManifest` exigem um **Full
   Restart** (Stop e Start), o Hot Reload não aplica permissões novas.
3. **Foco no Essencial**: Como os alunos vêm do trabalho, foque primeiro na
   Galeria (que funciona melhor em emulador) e deixe a Câmera para quem tem
   cabo/celular disponível.

## Registro e Coleta da Aula

- Atividade associada:
  [Atividade 10 - Câmera/Galeria + Permissões](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-10)
- Formulário:
  [Formulário Aula 10](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-10)

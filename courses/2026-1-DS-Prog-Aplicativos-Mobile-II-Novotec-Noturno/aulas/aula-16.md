---
layout: aula
title: "Aula 16 - Build, Publicação e Apresentação Final"
course_id: mobile2
category: aulas
---

## Data e contexto

- **Duração**: 5 horas-aula (250 minutos)
- **Laboratório**: 6 (Ambiente ETEC Noturno)
- **Pré-requisito**: Projeto Final Concluído

## Alinhamento com o PTD

- **Habilidades**: 1.1 a 1.5 (Todas as competências do semestre).
- **Bases**: empacotamento; distribuição; testes; apresentação final.

## Objetivos da aula (Professor)

- Gerar os arquivos binários finais (APK e App Bundle).
- Compreender o processo de publicação nas lojas oficiais (Google Play/App
  Store).
- Realizar a banca de apresentações e o fechamento do semestre.

## Roteiro por blocos (5 x 50 min)

### Bloco 1 (50 min): Preparação do Build (Release)

- **Configuração**: Alterar ícone do app, nome de exibição e Package Name único.
- **Assinatura**: Criar o `upload-keystore.jks` e configurar o `key.properties`.
- **Limpeza**: `flutter clean` para garantir que lixos de debug não entrem no
  build final.

### Bloco 2 (50 min): Gerando APK e AAB

- **Comandos**: `flutter build apk` e `flutter build appbundle`.
- **Análise**: Verificar o tamanho do arquivo final e onde ele foi salvo.
- **Distribuição Direta**: Enviar o APK para o próprio celular e instalar (fora
  da loja).

### Bloco 3 (50 min): O Ecossistema das Lojas

- **Teoria**: Como criar uma conta de desenvolvedor (Custos e Requisitos).
- **Processo**: Telas de print, política de privacidade, classificação etária e
  revisão.
- **Alternativas**: Firebase App Distribution e GitHub Releases para
  distribuição beta.

### Bloco 4 (50 min): Banca de Apresentações

- **Formato**: 5 minutos de "Pitch" + Demo funcional por grupo.
- **Critérios**: Funcionamento, Criatividade, Organização do Código e UI/UX.
- **Feedback**: Comentários rápidos dos colegas e do professor após cada demo.

### Bloco 5 (50 min): Autoavaliação e Encerramento

- **Atividade**: Preenchimento do formulário final de reflexão.
- **Organização**: Limpeza das máquinas do laboratório e entrega dos
  repositórios.
- **Fechamento**: Devolutiva geral da turma e celebração dos resultados.

## Guia para o Professor

- **Keystores**: Avise que se o aluno perder o arquivo da Keystore, ele nunca
  mais poderá atualizar o app na loja. É um documento vital.
- **Apresentação**: Foque no "código que funciona". Se o grupo não terminou
  tudo, peça para apresentarem o que foi feito com orgulho.
- **Rubrica**: Tenha uma planilha simples para anotar as notas/conceitos durante
  as apresentações para não esquecer detalhes.

## Estrutura do Formulário Google

1. **Nome Completo e Grupo**
2. **Link do Repositório Final (GitHub)**
3. **Autoavaliação**: O que você mais aprendeu neste semestre de Mobile II?
4. **Feedback**: O que poderia ser melhorado na infraestrutura ou no conteúdo
   das aulas?

## Dicas de Ouro (ETEC Noturno)

1. **Pen Drive ou Nuvem**: O build final (APK) pode ser pesado para o e-mail.
   Use Google Drive ou transfira via USB para o celular da apresentação.
2. **Backup da Key**: Insista para que os alunos subam o arquivo `.jks`
   (protegido) para um local seguro, ou explique por que ele não deve ir para o
   GitHub público.
3. **Portfólio Vivo**: Incentive os alunos a manterem o repositório organizado,
   pois este projeto é um excelente item de portfólio para entrevistas de
   estágio.

## Registro e Coleta da Aula

- Atividade associada:
  [Atividade 16 - Entrega e Apresentação Final](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-16)
- Formulário:
  [Formulário Aula 16](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-16)

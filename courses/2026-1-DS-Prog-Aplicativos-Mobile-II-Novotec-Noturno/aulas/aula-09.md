---
layout: aula
title: "Aula 09 - Consumo de API REST (Parte 2): POST, PUT e DELETE (CRUD)"
course_id: mobile2
category: aulas
---

## Data e contexto

- **Data:** 13/05/2026
- **Duração:** 5 horas-aula (250 min)
- **Horário:** 18h45 às 23h10 (considerando 15 min de intervalo)
- **Laboratório:** 6

## Alinhamento com o PTD

- **Habilidades:** 1.1, 1.3, 1.5
- **Bases:** Requisições HTTP (POST, PUT, DELETE); tratamento de respostas;
  integração com serviços externos; manipulação de estados.

---

## 1. Além do GET: Enviando Dados para a API (50 min)

### Conteúdo:

- O método `POST` e o corpo da requisição (Body).
- O método `toJson()` no modelo de dados.
- O Header `Content-Type: application/json`.

### Guia para o Professor:

- **Condução Técnica:** Explique que para o servidor entender o que estamos
  enviando, precisamos converter nosso objeto Dart em uma String JSON usando
  `jsonEncode(objeto.toJson())`.
- **Debugging:** Se o servidor retornar erro 400 (Bad Request), verifique se
  todos os campos obrigatórios estão sendo enviados e se o `Content-Type` está
  correto no Header.
- **Boas Práticas:** Use o `jsonEncode` apenas na camada de Service para manter
  a UI focada apenas nos dados.

---

## 2. Implementando o Cadastro (POST) (50 min)

### Conteúdo:

- Criação de um formulário simples para cadastro de um novo item (ex: Tarefa ou
  Produto).
- Chamada do método `create()` no `ApiService`.
- Tratamento de sucesso e retorno para a lista.

### Guia para o Professor:

- **Condução Técnica:** Reaproveite os conhecimentos da Aula 05 (Forms). Após o
  sucesso do POST, use `Navigator.pop(context, true)` para sinalizar à tela
  anterior que a lista precisa ser atualizada.
- **Debugging:** Se o novo item não aparecer na lista após voltar, verifique se
  você está chamando o `fetchData()` novamente no `then()` do Navigator.
- **Boas Práticas:** Mostre um `CircularProgressIndicator` sobreposto (Overlay)
  para impedir que o usuário clique no botão de "Salvar" várias vezes.

---

## 3. Edição e Exclusão: PUT e DELETE (50 min)

### Conteúdo:

- O conceito de `ID` como identificador único.
- Requisição `DELETE` para remover um item.
- Requisição `PUT` ou `PATCH` para atualizar dados existentes.

### Guia para o Professor:

- **Condução Técnica:** O `DELETE` geralmente não precisa de um corpo (Body),
  apenas do ID na URL (ex: `/produtos/1`). Já o `PUT` envia o objeto completo
  atualizado.
- **Debugging:** Erro comum: Tentar deletar um item e a API retornar 404.
  Verifique se o ID está sendo passado corretamente na interpolação da String da
  URL.
- **Boas Práticas:** Sempre peça uma confirmação (`showDialog`) antes de
  executar uma exclusão definitiva.

---

## 4. Atualização de UI e Feedback ao Usuário (50 min)

### Conteúdo:

- Removendo itens da lista local (`List.removeWhere`).
- Uso do `SnackBar` para confirmar ações de CRUD.
- Diferença entre "Optimistic UI" vs "Pessimistic UI".

### Guia para o Professor:

- **Condução Técnica:** Explique que o ideal é esperar a resposta da API
  (Pessimistic) antes de remover o item da tela, para garantir que a exclusão
  realmente ocorreu no servidor.
- **Debugging:** Se o SnackBar não aparecer após a exclusão, verifique se o
  `context` ainda é válido após o fechamento do diálogo de confirmação.
- **Boas Práticas:** Use cores padrão: Verde para sucesso (Criado/Editado) e
  Vermelho para erros ou exclusões.

---

## 5. Prática Guiada: O Mini-CRUD Funcional (50 min)

### Conteúdo:

- Desafio: Finalizar o fluxo de Adicionar e Excluir itens da lista consumindo a
  API.
- Testar o fluxo completo no dispositivo.

### Guia para o Professor:

- **Condução Técnica:** Este é o ápice do consumo de APIs. Garanta que o aluno
  entenda que o App é agora um espelho do banco de dados remoto.
- **Debugging:** Se a API de teste (ex: JSONPlaceholder) não salvar os dados de
  verdade (por ser apenas um Mock), explique que o status 201 (Created) é o
  sinal de sucesso que devemos tratar.
- **Encerramento:** Peça para os alunos demonstrarem um item sendo "criado" e
  outro sendo "deletado".

---

## Estrutura do Formulário (Google Forms)

| Ordem | Pergunta                                                                        | Tipo de Resposta | Observação Técnica            |
| :---- | :------------------------------------------------------------------------------ | :--------------- | :---------------------------- |
| 1     | Nome Completo                                                                   | Resposta curta   | Identificação                 |
| 2     | Qual método HTTP é utilizado para CRIAR um novo registro no servidor?           | Múltipla Escolha | `POST`                        |
| 3     | Qual método HTTP é utilizado para REMOVER um registro?                          | Múltipla Escolha | `DELETE`                      |
| 4     | O que o código HTTP 201 (Created) indica?                                       | Múltipla Escolha | Sucesso na criação do recurso |
| 5     | Link ou Print do seu App exibindo um SnackBar de sucesso após um POST ou DELETE | Upload / Link    | Evidência de fluxo completo   |

---

## Dicas de Ouro para o Professor (Lab Noturno)

1. **Simulação de Latência:** Às vezes a rede do lab é rápida demais para ver o
   loading. Use o "Network Link Conditioner" ou apenas um `Future.delayed` para
   que os alunos vejam o estado de carregamento e entendam a importância da
   experiência do usuário.
2. **Logs de Erro:** Ensine os alunos a usarem `print('Erro: $e')` no bloco
   `catch`. No noturno, é comum o cansaço fazer o aluno esquecer o básico do
   debug. Ter o erro impresso no console agiliza 100% o suporte do professor.
3. **Foco no "Caminho Feliz":** Se o tempo estiver curto, priorize o POST e o
   DELETE. O PUT (edição) pode ser deixado como desafio ou para a aula de
   reforço, pois a lógica é muito similar ao POST.

## Materiais Relacionados

- [Material 04 - Consumo de APIs REST](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-04)
- [Atividade 08 - Consumo de API Parte 1](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-08)

---

**Material elaborado para o curso de PAM2 - 2026**  
Prof. Gustavo Villalta

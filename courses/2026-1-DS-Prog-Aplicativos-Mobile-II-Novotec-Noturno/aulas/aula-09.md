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

## Objetivo da noite

Ao final da aula, você deve conseguir evoluir o app da Aula 08 para enviar dados
para uma API REST e executar um mini CRUD.

O foco de hoje é entender este caminho:

1. o app transforma um objeto Dart em JSON com `toJson`;
2. o service envia esse JSON com `POST`;
3. a API responde com um código HTTP, como `201 Created`;
4. o app mostra feedback para o usuário com `SnackBar`;
5. o app remove um registro usando `DELETE` com o `id` na URL;
6. o app confirma ações destrutivas antes de executar.

Nesta aula, `POST` e `DELETE` são obrigatórios. `PUT` fica como desafio extra se
o fluxo principal já estiver funcionando.

---

## O que você vai construir hoje

Você vai continuar o app da Aula 08, que já lista usuários vindos de:

```text
https://jsonplaceholder.typicode.com/users
```

Hoje o app deve ganhar:

- método `toJson` no modelo `Usuario`;
- método `criarUsuario` no `ApiService`;
- método `deletarUsuario` no `ApiService`;
- tela simples para cadastrar nome e e-mail;
- botão para excluir um usuário da lista;
- `showDialog` antes da exclusão;
- `SnackBar` depois de criar ou excluir.

> Importante: JSONPlaceholder é uma API de testes. Ela responde como se tivesse
> criado ou removido o registro, mas não salva os dados de verdade. Para esta
> aula, o que vale é a requisição correta, o status HTTP e o feedback no app.

---

## Materiais necessários

Antes de começar, deixe estes materiais abertos:

- [Aula 08 - API REST Parte 1](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/aulas/aula-08)
- [Material 04 - Consumo de APIs REST](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-04)

Você também precisa de:

- projeto Flutter da Aula 08 funcionando;
- pacote `http` instalado;
- permissão de internet no Android;
- arquivo `lib/models/usuario.dart`;
- arquivo `lib/services/api_service.dart`;
- tela de lista de usuários funcionando;
- emulador, celular ou navegador para testar o app.

Se a Aula 08 não estiver funcionando, volte para a Aula 08 primeiro. A Aula 09
depende da lista com `GET`.

---

## Documentação oficial para consulta

- [Flutter - Send data to the internet](https://docs.flutter.dev/cookbook/networking/send-data)
- [Flutter - Delete data on the internet](https://docs.flutter.dev/cookbook/networking/delete-data)
- [Pacote `http`](https://pub.dev/packages/http)
- [`Form`](https://api.flutter.dev/flutter/widgets/Form-class.html)
- [`TextFormField`](https://api.flutter.dev/flutter/material/TextFormField-class.html)
- [`SnackBar`](https://api.flutter.dev/flutter/material/SnackBar-class.html)
- [`showDialog`](https://api.flutter.dev/flutter/material/showDialog.html)
- [`Navigator`](https://api.flutter.dev/flutter/widgets/Navigator-class.html)
- [`jsonEncode`](https://api.flutter.dev/flutter/dart-convert/jsonEncode.html)

---

## Conceitos que você precisa dominar hoje

Antes de escrever código, entenda o que muda da Aula 08 para a Aula 09.

Na Aula 08, o app apenas lia dados. Ele fazia uma requisição `GET`, recebia uma
resposta em JSON e mostrava a lista na tela. Hoje o app vai tentar alterar dados
no servidor. Isso exige mais cuidado, porque a tela não pode fingir que salvou
ou excluiu alguma coisa sem antes entender a resposta da API.

### 1. Recurso, endpoint e ID

Em uma API REST, normalmente trabalhamos com **recursos**. Um usuário, uma
tarefa, um produto ou um pedido são exemplos de recursos.

No JSONPlaceholder, o recurso de usuários fica neste endpoint:

```text
/users
```

Quando queremos falar de um usuário específico, usamos o `id`:

```text
/users/1
```

Leia assim:

- `/users`: coleção de usuários;
- `/users/1`: usuário com ID 1;
- `/users/7`: usuário com ID 7.

Esse padrão é importante para o `DELETE` e para o `PUT`, porque essas operações
precisam saber qual registro será alterado.

### 2. Métodos HTTP e intenção da requisição

O método HTTP diz para a API qual é a intenção do app.

| Método   | Intenção               | Exemplo de URL | Corpo JSON?              | Resposta comum |
| :------- | :--------------------- | :------------- | :----------------------- | :------------- |
| `GET`    | Ler dados              | `/users`       | Não                      | `200 OK`       |
| `POST`   | Criar um novo registro | `/users`       | Sim                      | `201 Created`  |
| `PUT`    | Substituir/atualizar   | `/users/1`     | Sim                      | `200 OK`       |
| `PATCH`  | Atualizar parcialmente | `/users/1`     | Sim, com poucos campos   | `200 OK`       |
| `DELETE` | Remover um registro    | `/users/1`     | Normalmente não          | `200 OK`       |

O erro mais comum é tratar todos os métodos como se fossem iguais. Eles não são.
`POST` normalmente usa a URL da coleção (`/users`). `DELETE` normalmente usa a
URL do item (`/users/1`).

### 3. Corpo da requisição

No `GET`, a informação principal vai na URL. No `POST` e no `PUT`, a informação
principal vai no corpo da requisição.

Exemplo de corpo JSON para criar um usuário:

```json
{
  "name": "Maria Silva",
  "email": "maria@email.com"
}
```

No Flutter, você não deve montar esse texto JSON manualmente. O fluxo correto é:

1. criar um objeto Dart;
2. transformar esse objeto em `Map<String, dynamic>` com `toJson`;
3. transformar o mapa em texto JSON com `jsonEncode`;
4. enviar esse texto no `body` da requisição.

O caminho fica assim:

```text
Usuario -> toJson() -> Map -> jsonEncode() -> String JSON -> HTTP body
```

### 4. Header `Content-Type`

Quando o app envia JSON, ele precisa avisar isso para a API:

```dart
headers: {'Content-Type': 'application/json'}
```

Sem esse header, algumas APIs reais não conseguem interpretar o corpo da
requisição corretamente. O JSONPlaceholder é tolerante, mas sistemas reais
costumam ser mais rígidos.

### 5. Status code não é detalhe

O status HTTP é a forma como a API diz se a operação funcionou.

| Status | Significado                       | Como o app deve reagir                         |
| :----- | :-------------------------------- | :--------------------------------------------- |
| `200`  | Operação concluída com sucesso    | Atualizar a tela e mostrar feedback positivo   |
| `201`  | Registro criado com sucesso       | Voltar para a lista ou mostrar item criado     |
| `400`  | Dados inválidos                   | Mostrar erro claro para corrigir o formulário  |
| `401`  | Usuário não autenticado           | Pedir login novamente                          |
| `403`  | Sem permissão                     | Informar que a ação não é permitida            |
| `404`  | Recurso não encontrado            | Conferir URL e `id`                            |
| `500`  | Erro no servidor                  | Mostrar erro e permitir tentar novamente       |

Na Aula 09, o `POST` deve esperar `201`. O `DELETE` no JSONPlaceholder responde
com `200`.

### 6. API de testes vs API real

O JSONPlaceholder é ótimo para aprender porque responde rápido e não exige
login. Mas ele é uma API falsa para escrita: ela simula criação, atualização e
exclusão.

Isso significa:

- o `POST` pode retornar `201`, mas o usuário não fica salvo na API;
- o `DELETE` pode retornar `200`, mas o usuário volta se a lista for carregada
  de novo;
- o objetivo da aula é validar a requisição, o status e o comportamento da UI.

Em uma API real, depois de criar ou excluir, o banco de dados mudaria. Por isso
o app precisa ser organizado em camadas desde agora.

### 7. Camadas do app

Hoje cada arquivo tem uma responsabilidade:

| Camada             | Arquivo provável                         | Responsabilidade                                      |
| :----------------- | :--------------------------------------- | :---------------------------------------------------- |
| Modelo             | `lib/models/usuario.dart`                | Representar os dados e converter JSON                 |
| Service            | `lib/services/api_service.dart`          | Fazer requisições HTTP e interpretar status codes     |
| Tela de lista      | `lib/screens/usuarios_screen.dart`       | Mostrar usuários, loading, erro, cadastro e exclusão  |
| Tela de formulário | `lib/screens/cadastro_usuario_screen.dart` | Validar entrada do usuário e chamar o service       |

A tela não deve montar URL, header e JSON diretamente. Esse trabalho fica no
service. Assim, se a API mudar, você mexe menos na interface.

### 8. Estado da interface durante operações assíncronas

Requisições HTTP são assíncronas. O app pede algo para a internet e precisa
esperar a resposta.

Enquanto espera, a interface precisa proteger o usuário de ações duplicadas:

- desabilitar o botão enquanto salva;
- evitar dois `POST` seguidos por clique duplo;
- mostrar loading ou texto como `Salvando...`;
- exibir erro se a operação falhar.

Também usamos `mounted` antes de mexer na tela depois de um `await`. Isso evita
tentar mostrar `SnackBar` ou chamar `setState` em uma tela que já foi fechada.

### Perguntas de entendimento

Antes de seguir para o código, responda mentalmente:

- Por que `POST /users` cria, mas `DELETE /users/1` exclui?
- Por que o `POST` precisa de `body`, mas o `DELETE` normalmente não?
- Por que o app deve olhar o `statusCode` antes de mudar a tela?
- Por que uma API de testes pode retornar sucesso sem salvar de verdade?
- Qual camada do app deve conhecer a URL da API?

Se essas respostas ainda estiverem confusas, releia esta seção antes de
continuar.

---

## Mapa rápido da aula

Siga nesta ordem:

1. Conferir se a Aula 08 ainda lista usuários.
2. Adicionar `toJson` no modelo `Usuario`.
3. Adicionar `POST` no `ApiService`.
4. Criar uma tela de cadastro.
5. Abrir a tela de cadastro pelo botão `+`.
6. Mostrar `SnackBar` quando o cadastro funcionar.
7. Adicionar `DELETE` no `ApiService`.
8. Criar confirmação antes da exclusão.
9. Remover o item da lista local depois do sucesso.
10. Registrar as evidências da entrega no próprio repositório.

Não pule checkpoints. Se algo quebrar, volte para o último checkpoint que
funcionava.

---

## Bloco 1 - Conferir o ponto de partida

Rode o projeto da Aula 08:

```bash
flutter run
```

Abra a tela de usuários e confira se a lista carrega.

### Checkpoint 1

Antes de continuar:

- [ ] O app abre sem tela vermelha.
- [ ] A lista de usuários aparece.
- [ ] O projeto tem o pacote `http`.
- [ ] O projeto tem permissão de internet no Android.
- [ ] O service já tem um método de `GET`.

Se a lista não carrega, resolva isso antes de implementar `POST` e `DELETE`.

---

## Bloco 2 - Preparar o modelo para enviar JSON

Abra:

```text
lib/models/usuario.dart
```

Confira se a classe tem os campos `id`, `nome` e `email`. Depois adicione ou
ajuste o método `toJson`:

```dart
Map<String, dynamic> toJson() {
  return {
    'id': id,
    'name': nome,
    'email': email,
  };
}
```

O método `fromJson` transforma JSON em objeto Dart. O método `toJson` faz o
contrário: transforma objeto Dart em um mapa que pode virar JSON.

Pense nos dois métodos como portas de entrada e saída:

| Método     | Direção             | Usado quando                         |
| :--------- | :------------------ | :----------------------------------- |
| `fromJson` | JSON -> objeto Dart | A API responde dados para o app      |
| `toJson`   | objeto Dart -> JSON | O app envia dados para a API         |

Se você só tem `fromJson`, seu app sabe ler dados. Para criar ou atualizar, ele
também precisa saber escrever dados no formato que a API espera.

### Checkpoint 2

- [ ] O arquivo `usuario.dart` tem `fromJson`.
- [ ] O arquivo `usuario.dart` tem `toJson`.
- [ ] O app ainda compila depois dessa alteração.
- [ ] Você consegue explicar a diferença entre `fromJson` e `toJson`.

---

## Bloco 3 - Criar o método POST no service

Abra:

```text
lib/services/api_service.dart
```

Confira se existem estes imports:

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;
import '../models/usuario.dart';
```

Dentro da classe `ApiService`, adicione:

```dart
static Future<Usuario> criarUsuario(Usuario usuario) async {
  final response = await http.post(
    Uri.parse('$baseUrl/users'),
    headers: {'Content-Type': 'application/json'},
    body: jsonEncode(usuario.toJson()),
  );

  if (response.statusCode == 201) {
    return Usuario.fromJson(jsonDecode(response.body));
  }

  throw Exception('Erro ao criar usuario: ${response.statusCode}');
}
```

Se seu service usa `json.decode` em vez de `jsonDecode`, pode manter o padrão do
seu arquivo. O importante é converter o corpo da requisição para JSON.

Observe a responsabilidade de cada linha:

| Parte do código                                      | Função                                                        |
| :--------------------------------------------------- | :------------------------------------------------------------ |
| `http.post(...)`                                     | Define que a intenção é criar um recurso                      |
| `Uri.parse('$baseUrl/users')`                        | Converte a URL em um objeto `Uri` aceito pelo pacote `http`   |
| `headers: {'Content-Type': 'application/json'}`      | Avisa que o corpo está em JSON                                |
| `body: jsonEncode(usuario.toJson())`                 | Transforma o objeto em texto JSON para enviar                 |
| `response.statusCode == 201`                         | Confirma que a API aceitou a criação                          |
| `Usuario.fromJson(jsonDecode(response.body))`        | Converte a resposta da API de volta para objeto Dart          |
| `throw Exception(...)`                               | Faz a tela saber que a operação falhou                        |

Em uma aplicação maior, o service poderia retornar uma classe de resultado com
mensagem, dados e status. Para esta aula, lançar `Exception` é suficiente para
treinar o fluxo de sucesso e erro.

### Checkpoint 3

- [ ] O método usa `http.post`.
- [ ] A URL termina em `/users`.
- [ ] O header tem `Content-Type: application/json`.
- [ ] O body usa `usuario.toJson`.
- [ ] O sucesso espera status `201`.
- [ ] O erro inclui o `statusCode` para ajudar no debug.

---

## Bloco 4 - Criar a tela de cadastro

Crie o arquivo:

```text
lib/screens/cadastro_usuario_screen.dart
```

Use este modelo:

```dart
import 'package:flutter/material.dart';
import '../models/usuario.dart';
import '../services/api_service.dart';

class CadastroUsuarioScreen extends StatefulWidget {
  const CadastroUsuarioScreen({super.key});

  @override
  State<CadastroUsuarioScreen> createState() => _CadastroUsuarioScreenState();
}

class _CadastroUsuarioScreenState extends State<CadastroUsuarioScreen> {
  final _formKey = GlobalKey<FormState>();
  final _nomeController = TextEditingController();
  final _emailController = TextEditingController();
  bool _salvando = false;

  @override
  void dispose() {
    _nomeController.dispose();
    _emailController.dispose();
    super.dispose();
  }

  Future<void> _salvar() async {
    if (!_formKey.currentState!.validate()) return;

    setState(() => _salvando = true);

    final usuario = Usuario(
      id: 0,
      nome: _nomeController.text,
      email: _emailController.text,
    );

    try {
      await ApiService.criarUsuario(usuario);

      if (!mounted) return;

      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('Usuario criado com sucesso')),
      );

      Navigator.pop(context, true);
    } catch (e) {
      if (!mounted) return;

      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('Erro ao criar usuario: $e')),
      );
    } finally {
      if (mounted) {
        setState(() => _salvando = false);
      }
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Novo usuario')),
      body: Padding(
        padding: const EdgeInsets.all(16),
        child: Form(
          key: _formKey,
          child: Column(
            children: [
              TextFormField(
                controller: _nomeController,
                decoration: const InputDecoration(labelText: 'Nome'),
                validator: (value) {
                  if (value == null || value.trim().isEmpty) {
                    return 'Informe o nome';
                  }
                  return null;
                },
              ),
              TextFormField(
                controller: _emailController,
                decoration: const InputDecoration(labelText: 'E-mail'),
                validator: (value) {
                  if (value == null || value.trim().isEmpty) {
                    return 'Informe o e-mail';
                  }
                  return null;
                },
              ),
              const SizedBox(height: 24),
              SizedBox(
                width: double.infinity,
                child: ElevatedButton(
                  onPressed: _salvando ? null : _salvar,
                  child: Text(_salvando ? 'Salvando...' : 'Salvar'),
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

Se sua classe `Usuario` exige outros campos, preencha com valores temporários ou
ajuste o construtor.

Essa tela tem quatro ideias importantes:

- `TextEditingController` guarda o que o usuário digitou;
- `Form` e `validator` impedem envio vazio;
- `_salvando` evita clique duplo no botão;
- `try/catch/finally` separa sucesso, erro e limpeza do estado.

O bloco `finally` roda tanto quando dá certo quanto quando dá erro. Por isso ele
é um bom lugar para desligar o estado de salvamento.

### Checkpoint 4

- [ ] A tela de cadastro compila.
- [ ] O botão Salvar valida campos vazios.
- [ ] Enquanto salva, o botão fica desabilitado.
- [ ] Em sucesso, aparece `SnackBar`.
- [ ] Em erro, aparece `SnackBar` com mensagem de falha.

---

## Bloco 5 - Abrir o cadastro pela tela de lista

Abra a tela que lista os usuários, por exemplo:

```text
lib/screens/usuarios_screen.dart
```

Adicione o import:

```dart
import 'cadastro_usuario_screen.dart';
```

No `FloatingActionButton`, navegue para a tela de cadastro:

```dart
floatingActionButton: FloatingActionButton(
  onPressed: () async {
    final criou = await Navigator.push<bool>(
      context,
      MaterialPageRoute(
        builder: (context) => const CadastroUsuarioScreen(),
      ),
    );

    if (criou == true) {
      _carregarUsuarios();
    }
  },
  child: const Icon(Icons.add),
),
```

Se o nome do seu método de carregar lista for diferente de `_carregarUsuarios`,
use o nome que existe no seu projeto.

O `Navigator.push<bool>` espera receber um valor booleano quando a tela de
cadastro fechar. No nosso caso:

- `true`: o cadastro funcionou, então a lista pode ser recarregada;
- `null` ou `false`: o usuário voltou sem criar nada.

Esse padrão evita recarregar a lista sem necessidade.

### Checkpoint 5

- [ ] O botão `+` abre a tela de cadastro.
- [ ] O cadastro volta para a lista depois de salvar.
- [ ] O app chama o service com `POST`.
- [ ] A lista é recarregada depois do cadastro.
- [ ] Se você voltar sem salvar, a lista não precisa recarregar.

---

## Bloco 6 - Criar o método DELETE no service

No `ApiService`, adicione:

```dart
static Future<void> deletarUsuario(int id) async {
  final response = await http.delete(
    Uri.parse('$baseUrl/users/$id'),
  );

  if (response.statusCode != 200) {
    throw Exception('Erro ao deletar usuario: ${response.statusCode}');
  }
}
```

O `DELETE` usa o `id` na URL. Exemplo:

```text
https://jsonplaceholder.typicode.com/users/1
```

Perceba que o `DELETE` não recebe `Usuario` inteiro. Ele só precisa identificar
qual recurso será removido. Por isso o parâmetro é `int id`.

Em uma API real, o servidor poderia responder:

- `200`: excluído e resposta com algum conteúdo;
- `204`: excluído sem corpo de resposta;
- `404`: ID não encontrado;
- `403`: usuário logado não pode excluir aquele recurso.

Para simplificar com JSONPlaceholder, vamos aceitar `200`. Se você quiser deixar
o código mais próximo de APIs reais, pode aceitar `200` ou `204`.

### Checkpoint 6

- [ ] O método usa `http.delete`.
- [ ] A URL inclui o `id`.
- [ ] O método lança erro se o status não for `200`.
- [ ] Você consegue explicar por que o `DELETE` recebe apenas o `id`.

---

## Bloco 7 - Confirmar e excluir pela lista

Na tela de usuários, crie um método para confirmar a exclusão:

```dart
Future<void> _confirmarExclusao(Usuario usuario) async {
  final confirmar = await showDialog<bool>(
    context: context,
    builder: (context) {
      return AlertDialog(
        title: const Text('Excluir usuario'),
        content: Text('Deseja excluir ${usuario.nome}?'),
        actions: [
          TextButton(
            onPressed: () => Navigator.pop(context, false),
            child: const Text('Cancelar'),
          ),
          TextButton(
            onPressed: () => Navigator.pop(context, true),
            child: const Text('Excluir'),
          ),
        ],
      );
    },
  );

  if (confirmar != true) return;

  try {
    await ApiService.deletarUsuario(usuario.id);

    setState(() {
      _usuarios.removeWhere((item) => item.id == usuario.id);
    });

    if (!mounted) return;

    ScaffoldMessenger.of(context).showSnackBar(
      const SnackBar(content: Text('Usuario excluido com sucesso')),
    );
  } catch (e) {
    if (!mounted) return;

    ScaffoldMessenger.of(context).showSnackBar(
      SnackBar(content: Text('Erro ao excluir usuario: $e')),
    );
  }
}
```

No item da lista, adicione um botão de excluir:

```dart
trailing: IconButton(
  icon: const Icon(Icons.delete),
  onPressed: () => _confirmarExclusao(usuario),
),
```

Se sua lista já usa `trailing` para outro ícone, troque por uma `Row` pequena ou
substitua o ícone antigo temporariamente.

Aqui existem duas estratégias possíveis de UI:

| Estratégia       | Como funciona                                                | Quando usar                                      |
| :--------------- | :----------------------------------------------------------- | :---------------------------------------------- |
| Pessimista       | Espera a API responder e só depois muda a tela               | Mais segura para iniciantes e sistemas críticos |
| Otimista         | Muda a tela antes e desfaz se a API falhar                   | Melhor UX, mas exige mais controle de erro      |

Nesta aula usamos a estratégia pessimista: primeiro esperamos
`ApiService.deletarUsuario`, depois removemos da lista local.

Isso evita mostrar para o usuário que algo foi excluído quando a API retornou
erro.

### Checkpoint 7

- [ ] Cada item da lista tem botão de excluir.
- [ ] O app pergunta antes de excluir.
- [ ] O `DELETE` é chamado somente depois da confirmação.
- [ ] O item sai da lista depois do sucesso.
- [ ] O app mostra `SnackBar`.
- [ ] Se a API falhar, o item continua na lista.

---

## Bloco 8 - Desafio opcional: PUT

Faça este bloco apenas se `POST` e `DELETE` já estiverem funcionando.

No `ApiService`, adicione:

```dart
static Future<Usuario> atualizarUsuario(Usuario usuario) async {
  final response = await http.put(
    Uri.parse('$baseUrl/users/${usuario.id}'),
    headers: {'Content-Type': 'application/json'},
    body: jsonEncode(usuario.toJson()),
  );

  if (response.statusCode == 200) {
    return Usuario.fromJson(jsonDecode(response.body));
  }

  throw Exception('Erro ao atualizar usuario: ${response.statusCode}');
}
```

O `PUT` atualiza um registro existente. Ele se parece com o `POST`, mas usa o
`id` na URL.

Diferença prática:

- `POST /users`: cria um novo usuário dentro da coleção;
- `PUT /users/1`: substitui os dados do usuário 1.

Em muitas APIs, `PUT` exige o objeto completo. Se você enviar só o e-mail, a API
pode apagar os outros campos. Quando a API permite atualizar só alguns campos,
normalmente ela oferece `PATCH`.

---

## Revisão guiada do fluxo completo

Quando o app estiver funcionando, acompanhe uma criação de usuário do começo ao
fim:

1. usuário digita nome e e-mail;
2. tela valida os campos;
3. tela cria um objeto `Usuario`;
4. tela chama `ApiService.criarUsuario`;
5. service chama `usuario.toJson`;
6. service chama `jsonEncode`;
7. pacote `http` envia `POST /users`;
8. API responde `201`;
9. service converte a resposta com `fromJson`;
10. tela mostra `SnackBar`;
11. tela fecha com `Navigator.pop(context, true)`;
12. lista recarrega.

Agora acompanhe uma exclusão:

1. usuário toca no ícone de excluir;
2. app abre `showDialog`;
3. usuário confirma;
4. tela chama `ApiService.deletarUsuario(usuario.id)`;
5. service envia `DELETE /users/{id}`;
6. API responde `200`;
7. tela remove o item da lista local;
8. tela mostra `SnackBar`.

Se você consegue narrar esses dois fluxos sem olhar o código, você entendeu o
conteúdo central da aula.

---

## Questões para discussão ou registro no caderno

1. Qual é a diferença entre enviar dados no corpo da requisição e enviar dados
   na URL?
2. Por que o service é um lugar melhor para requisições HTTP do que a tela?
3. O que poderia acontecer se o app removesse o item da lista antes da API
   responder?
4. Por que uma API real pode exigir autenticação para `POST`, `PUT` e `DELETE`,
   mesmo que o `GET` seja público?
5. Em que situação `PATCH` seria melhor que `PUT`?
6. Por que o app precisa mostrar erro para o usuário em vez de apenas imprimir
   no console?

---

## Erros comuns

| Problema                                     | Onde verificar                                                        |
| :------------------------------------------- | :-------------------------------------------------------------------- |
| Erro 400 ou 500 no `POST`                    | Confira o `body` e o header `Content-Type: application/json`.          |
| Erro 404 no `DELETE`                         | Confira se o `id` está entrando na URL.                               |
| `jsonEncode` não encontrado                  | Confira o import `dart:convert`.                                      |
| O `SnackBar` não aparece                     | Confira se o código roda antes de fechar a tela ou se `mounted` vale. |
| O app salva, mas o usuário não aparece na API | JSONPlaceholder não persiste dados; isso é esperado.                  |
| O item volta depois de recarregar a lista    | JSONPlaceholder não remove dados de verdade; isso é esperado.         |
| Dois usuários são criados com clique duplo    | Desabilite o botão enquanto `_salvando` for `true`.                   |
| Erro após fechar a tela                       | Confira se existe `if (!mounted) return;` depois de `await`.          |
| A tela sabe detalhes demais da API            | Mova URL, headers e status codes para o `ApiService`.                 |

---

## Entrega da aula

Esta entrega está embutida neste roteiro. Não existe arquivo separado de
atividade nem formulário separado para a Aula 09.

O envio oficial deve ser feito pelo Google Forms:

- [Formulário de entrega da Aula 09](https://docs.google.com/forms/d/e/1FAIpQLSc5naYv_iX07p-Z_Siz1FfU3Voh-BbpPH5AcKCETqSNh7PF6g/viewform?usp=dialog)

### Objetivo da entrega

Evoluir o app da Aula 08 para executar pelo menos duas ações de escrita em uma
API REST:

- criar um registro com `POST`;
- remover um registro com `DELETE`.

O `PUT` é desafio extra, não requisito mínimo.

### Entrega mínima

Seu app deve demonstrar:

- [ ] lista da Aula 08 ainda funcionando com `GET`;
- [ ] `toJson` no modelo;
- [ ] `POST` funcionando com status `201`;
- [ ] tela de cadastro;
- [ ] `DELETE` funcionando com `id`;
- [ ] confirmação antes de excluir;
- [ ] `SnackBar` em sucesso e erro;
- [ ] link do repositório atualizado;
- [ ] evidências registradas no README, em uma pasta `evidencias/` ou em uma
      issue/descrição da entrega.

### Critérios de avaliação

- **3 pts**: `POST` implementado corretamente com JSON e status `201`;
- **2 pts**: `DELETE` implementado corretamente com `id` na URL;
- **2 pts**: UI com cadastro, confirmação de exclusão e feedback por `SnackBar`;
- **2 pts**: tratamento de carregamento/erro durante as ações;
- **1 pt**: organização do código em model, service e telas.

### Evidências esperadas

Registre no repositório:

- link ou print do cadastro funcionando;
- print do `SnackBar` após criar ou excluir;
- print do diálogo de confirmação antes de excluir;
- trecho ou arquivo do `ApiService` com `POST` e `DELETE`;
- explicação curta sobre por que o JSONPlaceholder retorna sucesso mas não
  persiste o registro;
- explicação curta da diferença entre `fromJson` e `toJson`;
- explicação curta sobre por que a exclusão deve esperar a resposta da API antes
  de remover o item da tela.

### Parte conceitual obrigatória

Além do app funcionando, responda no próprio repositório:

1. Qual é a diferença entre `POST /users` e `DELETE /users/1`?
2. Por que o `POST` precisa enviar `Content-Type: application/json`?
3. O que significa receber status `201`?
4. Por que a tela não deveria montar URL e JSON diretamente?
5. O que muda entre uma API de testes como JSONPlaceholder e uma API real com
   banco de dados?

### Checklist final

- [ ] O app ainda lista usuários com `GET`.
- [ ] O cadastro chama `POST` e recebe status `201`.
- [ ] O `DELETE` usa o `id` correto.
- [ ] Existe confirmação antes da exclusão.
- [ ] Existe `SnackBar` para sucesso e erro.
- [ ] O app não trava se a internet falhar.
- [ ] O repositório está atualizado.
- [ ] Você consegue explicar o fluxo completo de cadastro.
- [ ] Você consegue explicar o fluxo completo de exclusão.

## Materiais Relacionados

- [Material 04 - Consumo de APIs REST](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-04)

---

**Material elaborado para o curso de PAM2 - 2026**  
Prof. Gustavo Villalta

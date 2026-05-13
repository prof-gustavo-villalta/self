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
- [Atividade 09 - REST Parte 2 (Mini CRUD)](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-09)
- [Formulário Aula 09](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-09)

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
10. Registrar evidências e preencher a Atividade 09.

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

### Checkpoint 2

- [ ] O arquivo `usuario.dart` tem `fromJson`.
- [ ] O arquivo `usuario.dart` tem `toJson`.
- [ ] O app ainda compila depois dessa alteração.

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

### Checkpoint 3

- [ ] O método usa `http.post`.
- [ ] A URL termina em `/users`.
- [ ] O header tem `Content-Type: application/json`.
- [ ] O body usa `usuario.toJson`.
- [ ] O sucesso espera status `201`.

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

### Checkpoint 4

- [ ] A tela de cadastro compila.
- [ ] O botão Salvar valida campos vazios.
- [ ] Enquanto salva, o botão fica desabilitado.
- [ ] Em sucesso, aparece `SnackBar`.

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

### Checkpoint 5

- [ ] O botão `+` abre a tela de cadastro.
- [ ] O cadastro volta para a lista depois de salvar.
- [ ] O app chama o service com `POST`.
- [ ] A lista é recarregada depois do cadastro.

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

### Checkpoint 6

- [ ] O método usa `http.delete`.
- [ ] A URL inclui o `id`.
- [ ] O método lança erro se o status não for `200`.

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

### Checkpoint 7

- [ ] Cada item da lista tem botão de excluir.
- [ ] O app pergunta antes de excluir.
- [ ] O `DELETE` é chamado somente depois da confirmação.
- [ ] O item sai da lista depois do sucesso.
- [ ] O app mostra `SnackBar`.

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

---

## Entrega da aula

Para considerar a atividade pronta, você deve ter:

- [ ] lista da Aula 08 ainda funcionando com `GET`;
- [ ] `toJson` no modelo;
- [ ] `POST` funcionando com status `201`;
- [ ] tela de cadastro;
- [ ] `DELETE` funcionando com `id`;
- [ ] confirmação antes de excluir;
- [ ] `SnackBar` em sucesso e erro;
- [ ] link do repositório atualizado;
- [ ] evidências registradas para o formulário.

As evidências e perguntas estão em:

- [Atividade 09 - REST Parte 2 (Mini CRUD)](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-09)
- [Formulário Aula 09](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-09)

## Materiais Relacionados

- [Material 04 - Consumo de APIs REST](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-04)
- [Atividade 09 - REST Parte 2 (Mini CRUD)](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-09)
- [Formulário Aula 09](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-09)

---

**Material elaborado para o curso de PAM2 - 2026**  
Prof. Gustavo Villalta

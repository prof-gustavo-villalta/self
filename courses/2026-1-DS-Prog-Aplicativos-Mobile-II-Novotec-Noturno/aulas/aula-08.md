---
layout: aula
title: "Aula 08 - Consumo de API REST (Parte 1): HTTP, JSON e Modelos"
course_id: mobile2
category: aulas
---

## Data e contexto

- **Data:** 06/05/2026
- **Duração:** 5 horas-aula (250 min)
- **Horário:** 18h45 às 23h10 (considerando 15 min de intervalo)
- **Laboratório:** 6

## Alinhamento com o PTD

- **Habilidades:** 1.1, 1.3, 1.5
- **Bases:** Consumo de APIs REST; requisições HTTP (GET); serialização JSON;
  tratamento de erros e estados de carregamento.

---

## Objetivo da noite

Ao final da aula, você deve conseguir construir uma tela Flutter que busca dados
de uma API real na internet e mostra esses dados em uma lista.

O foco de hoje é entender o caminho completo:

1. o app faz uma requisição HTTP;
2. a API responde em JSON;
3. o Dart converte o JSON em objetos;
4. a tela mostra carregamento, sucesso ou erro;
5. a lista aparece com dados reais.

Nesta aula vamos usar apenas requisições `GET`. As operações de criar, atualizar
e apagar dados ficam para a Aula 09.

---

## O que você vai construir hoje

Você vai construir uma tela chamada **Usuarios** usando a API pública
JSONPlaceholder:

- endpoint: `https://jsonplaceholder.typicode.com/users`;
- pacote Flutter: `http`;
- modelo Dart: `Usuario`;
- service: `ApiService`;
- tela: `UsuariosScreen`;
- lista: `ListView.builder`.

No final, seu app deve mostrar nome, e-mail e cidade dos usuários retornados
pela API.

---

## Resultado esperado

Ao final da aula, seu app deve ter:

- dependência `http` instalada;
- permissão de internet no Android;
- classe `Usuario` com `fromJson`;
- classe `ApiService` buscando usuários da API;
- tela com `CircularProgressIndicator` enquanto carrega;
- mensagem de erro com botão para tentar novamente;
- lista de usuários reais quando a requisição funcionar.

---

## Antes de começar

Confirme que você tem:

- um projeto Flutter abrindo sem erro;
- VS Code ou Android Studio;
- emulador, celular ou navegador configurado para rodar o app;
- internet funcionando no computador;
- navegador para testar a URL da API.

Se você não tiver um projeto pronto, crie um novo:

```bash
flutter create aula08_api_rest
cd aula08_api_rest
flutter run
```

Se algo quebrar já nesse ponto, resolva o ambiente antes de continuar.

---

## Documentação oficial que será usada hoje

Use estes links como consulta durante a aula:

- [Flutter - Fetch data from the internet](https://docs.flutter.dev/cookbook/networking/fetch-data)
- [Flutter - Send data to the internet](https://docs.flutter.dev/cookbook/networking/send-data)
- [Pacote `http`](https://pub.dev/packages/http)
- [`FutureBuilder`](https://api.flutter.dev/flutter/widgets/FutureBuilder-class.html)
- [`CircularProgressIndicator`](https://api.flutter.dev/flutter/material/CircularProgressIndicator-class.html)
- [`ListView.builder`](https://api.flutter.dev/flutter/widgets/ListView/ListView.builder.html)
- [`ListTile`](https://api.flutter.dev/flutter/material/ListTile-class.html)
- [`Uri.parse`](https://api.flutter.dev/flutter/dart-core/Uri/parse.html)
- [`jsonDecode`](https://api.flutter.dev/flutter/dart-convert/jsonDecode.html)

---

## Mapa rápido da aula

Siga nesta ordem. Não pule etapas.

1. Testar a API no navegador.
2. Adicionar o pacote `http`.
3. Adicionar a permissão de internet no Android.
4. Criar o modelo `Usuario`.
5. Criar o service `ApiService`.
6. Criar a tela `UsuariosScreen`.
7. Ligar a tela no `main.dart`.
8. Rodar o app e validar loading, sucesso e erro.
9. Registrar evidências para a atividade.

Se algo quebrar, volte para o último checkpoint que funcionava.

---

## Bloco 1 - Entendendo a API

### Passo 1. Teste a URL no navegador

Abra esta URL no navegador:

```text
https://jsonplaceholder.typicode.com/users
```

Você deve ver uma lista em JSON parecida com esta:

```json
[
  {
    "id": 1,
    "name": "Leanne Graham",
    "email": "Sincere@april.biz",
    "address": {
      "city": "Gwenborough"
    }
  }
]
```

Observe três campos que vamos usar:

- `id`;
- `name`;
- `email`;
- `address.city`.

### Checkpoint 1

Antes de continuar, confirme:

- [ ] A URL abriu no navegador.
- [ ] Você encontrou o campo `name`.
- [ ] Você encontrou o campo `email`.
- [ ] Você encontrou o campo `city` dentro de `address`.

Se a URL não abrir na rede da escola, teste com a internet do celular ou avise o
professor.

---

## Bloco 2 - Preparando o projeto Flutter

### Passo 2. Adicione o pacote `http`

No terminal, dentro da pasta do projeto, execute:

```bash
flutter pub add http
```

Depois rode:

```bash
flutter pub get
```

Confira se o `pubspec.yaml` recebeu uma linha parecida com esta:

```yaml
dependencies:
  http: ^1.2.0
```

A versão pode ser diferente. O importante é o pacote `http` estar na lista.

### Passo 3. Adicione permissão de internet no Android

Abra o arquivo:

```text
android/app/src/main/AndroidManifest.xml
```

Dentro de `<manifest>`, antes de `<application>`, adicione:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

O início do arquivo deve ficar parecido com isto:

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
    <uses-permission android:name="android.permission.INTERNET" />

    <application
        android:label="aula08_api_rest"
        android:name="${applicationName}"
        android:icon="@mipmap/ic_launcher">
```

### Checkpoint 2

Antes de continuar, confirme:

- [ ] O comando `flutter pub add http` funcionou.
- [ ] O `pubspec.yaml` tem o pacote `http`.
- [ ] O `AndroidManifest.xml` tem a permissão de internet.
- [ ] O app ainda abre com `flutter run`.

---

## Bloco 3 - Criando o modelo de dados

### Passo 4. Crie a pasta de modelos

Dentro de `lib`, crie a pasta:

```text
lib/models
```

Dentro dela, crie o arquivo:

```text
lib/models/usuario.dart
```

Cole o código:

```dart
class Usuario {
  final int id;
  final String nome;
  final String email;
  final String cidade;

  Usuario({
    required this.id,
    required this.nome,
    required this.email,
    required this.cidade,
  });

  factory Usuario.fromJson(Map<String, dynamic> json) {
    final endereco = json['address'] as Map<String, dynamic>;

    return Usuario(
      id: json['id'] as int,
      nome: json['name'] as String,
      email: json['email'] as String,
      cidade: endereco['city'] as String,
    );
  }
}
```

### O que esse código faz

- `Usuario` representa um usuário da API dentro do app.
- `fromJson` converte o `Map<String, dynamic>` vindo da API em um objeto Dart.
- `address` é outro objeto dentro do JSON, por isso acessamos
  `json['address']` antes de pegar a cidade.

### Checkpoint 3

Antes de continuar, confirme:

- [ ] O arquivo `lib/models/usuario.dart` existe.
- [ ] A classe se chama `Usuario`.
- [ ] O método se chama `fromJson`.
- [ ] Não há erro de digitação no arquivo.

---

## Bloco 4 - Criando o service da API

### Passo 5. Crie a pasta de services

Dentro de `lib`, crie a pasta:

```text
lib/services
```

Dentro dela, crie o arquivo:

```text
lib/services/api_service.dart
```

Cole o código:

```dart
import 'dart:convert';

import 'package:http/http.dart' as http;

import '../models/usuario.dart';

class ApiService {
  static const String _baseUrl = 'https://jsonplaceholder.typicode.com';

  Future<List<Usuario>> buscarUsuarios() async {
    final uri = Uri.parse('$_baseUrl/users');

    final response = await http.get(uri);

    if (response.statusCode != 200) {
      throw Exception('Erro ao buscar usuarios: ${response.statusCode}');
    }

    final listaJson = jsonDecode(response.body) as List<dynamic>;

    return listaJson
        .map((item) => Usuario.fromJson(item as Map<String, dynamic>))
        .toList();
  }
}
```

### O que esse código faz

- `http.get(uri)` faz a requisição para a internet.
- `response.statusCode` informa se a API respondeu com sucesso.
- `jsonDecode(response.body)` transforma o texto JSON em dados que o Dart
  consegue ler.
- `map(...)` transforma cada item do JSON em um objeto `Usuario`.

### Checkpoint 4

Antes de continuar, confirme:

- [ ] O arquivo `lib/services/api_service.dart` existe.
- [ ] O import do pacote `http` não está vermelho.
- [ ] O import de `usuario.dart` está correto.
- [ ] O método se chama `buscarUsuarios`.

Se o import do `http` ficar vermelho, rode novamente:

```bash
flutter pub get
```

---

## Bloco 5 - Criando a tela de usuários

### Passo 6. Crie a pasta de telas

Dentro de `lib`, crie a pasta:

```text
lib/screens
```

Dentro dela, crie o arquivo:

```text
lib/screens/usuarios_screen.dart
```

Cole o código:

```dart
import 'package:flutter/material.dart';

import '../models/usuario.dart';
import '../services/api_service.dart';

class UsuariosScreen extends StatefulWidget {
  const UsuariosScreen({super.key});

  @override
  State<UsuariosScreen> createState() => _UsuariosScreenState();
}

class _UsuariosScreenState extends State<UsuariosScreen> {
  final _apiService = ApiService();

  List<Usuario> _usuarios = [];
  bool _carregando = true;
  String? _erro;

  @override
  void initState() {
    super.initState();
    _buscarUsuarios();
  }

  Future<void> _buscarUsuarios() async {
    setState(() {
      _carregando = true;
      _erro = null;
    });

    try {
      final usuarios = await _apiService.buscarUsuarios();

      setState(() {
        _usuarios = usuarios;
      });
    } catch (erro) {
      setState(() {
        _erro = 'Nao foi possivel carregar os usuarios.';
      });
    } finally {
      setState(() {
        _carregando = false;
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Usuarios da API'),
        actions: [
          IconButton(
            onPressed: _buscarUsuarios,
            icon: const Icon(Icons.refresh),
            tooltip: 'Recarregar',
          ),
        ],
      ),
      body: _buildBody(),
    );
  }

  Widget _buildBody() {
    if (_carregando) {
      return const Center(
        child: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            CircularProgressIndicator(),
            SizedBox(height: 16),
            Text('Carregando usuarios...'),
          ],
        ),
      );
    }

    if (_erro != null) {
      return Center(
        child: Padding(
          padding: const EdgeInsets.all(24),
          child: Column(
            mainAxisSize: MainAxisSize.min,
            children: [
              const Icon(
                Icons.wifi_off,
                size: 56,
                color: Colors.red,
              ),
              const SizedBox(height: 16),
              Text(
                _erro!,
                textAlign: TextAlign.center,
              ),
              const SizedBox(height: 16),
              ElevatedButton.icon(
                onPressed: _buscarUsuarios,
                icon: const Icon(Icons.refresh),
                label: const Text('Tentar novamente'),
              ),
            ],
          ),
        ),
      );
    }

    if (_usuarios.isEmpty) {
      return const Center(
        child: Text('Nenhum usuario encontrado.'),
      );
    }

    return ListView.separated(
      itemCount: _usuarios.length,
      separatorBuilder: (context, index) => const Divider(height: 1),
      itemBuilder: (context, index) {
        final usuario = _usuarios[index];

        return ListTile(
          leading: CircleAvatar(
            child: Text(usuario.nome.substring(0, 1)),
          ),
          title: Text(usuario.nome),
          subtitle: Text('${usuario.email}\n${usuario.cidade}'),
          isThreeLine: true,
        );
      },
    );
  }
}
```

### Checkpoint 5

Antes de continuar, confirme:

- [ ] O arquivo `lib/screens/usuarios_screen.dart` existe.
- [ ] Os imports não estão vermelhos.
- [ ] A classe se chama `UsuariosScreen`.
- [ ] Existe um `CircularProgressIndicator`.
- [ ] Existe um botão `Tentar novamente`.

---

## Bloco 6 - Ligando a tela no app

### Passo 7. Atualize o `main.dart`

Abra:

```text
lib/main.dart
```

Substitua o conteúdo por:

```dart
import 'package:flutter/material.dart';

import 'screens/usuarios_screen.dart';

void main() {
  runApp(const MeuApp());
}

class MeuApp extends StatelessWidget {
  const MeuApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Aula 08 - API REST',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.teal),
        useMaterial3: true,
      ),
      home: const UsuariosScreen(),
    );
  }
}
```

### Passo 8. Rode o app

No terminal:

```bash
flutter run
```

O app deve abrir mostrando:

1. uma tela de carregamento;
2. depois uma lista de usuários;
3. botão de recarregar no topo.

### Checkpoint 6

Antes de considerar a atividade pronta, confirme:

- [ ] O app abre sem tela vermelha.
- [ ] Aparece o texto `Carregando usuarios...`.
- [ ] A lista aparece com nomes reais.
- [ ] Cada item mostra e-mail.
- [ ] Cada item mostra cidade.
- [ ] O botão de recarregar funciona.

---

## Bloco 7 - Testando erro de rede

### Passo 9. Simule um erro

No arquivo `lib/services/api_service.dart`, altere temporariamente:

```dart
static const String _baseUrl = 'https://jsonplaceholder.typicode.com';
```

para:

```dart
static const String _baseUrl = 'https://jsonplaceholder.typicode.com/erro';
```

Rode o app novamente. Ele deve mostrar a mensagem de erro e o botão
`Tentar novamente`.

Depois do teste, volte para a URL correta:

```dart
static const String _baseUrl = 'https://jsonplaceholder.typicode.com';
```

### Checkpoint 7

Antes de enviar, confirme:

- [ ] Você viu a tela de erro pelo menos uma vez.
- [ ] O botão `Tentar novamente` aparece.
- [ ] A URL correta foi restaurada.
- [ ] A lista voltou a funcionar.

---

## Erros comuns e como resolver

### `Target of URI doesn't exist: package:http/http.dart`

O pacote `http` não foi instalado ou o VS Code ainda não atualizou.

Rode:

```bash
flutter pub get
```

Se continuar, feche e abra o VS Code.

### Tela fica carregando para sempre

Verifique se o `finally` existe no método `_buscarUsuarios`:

```dart
finally {
  setState(() {
    _carregando = false;
  });
}
```

### Erro de permissão ou app não busca dados no Android

Confira se o arquivo `AndroidManifest.xml` tem:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

Essa linha deve ficar antes de `<application>`.

### `type 'Null' is not a subtype of type 'String'`

Algum campo esperado não veio no JSON. Confira se você digitou corretamente:

```dart
json['name']
json['email']
endereco['city']
```

### A escola bloqueou a API

Teste no navegador. Se a URL também não abrir no navegador, tente:

- internet do celular;
- outro endpoint da lista do Material 04;
- pedir ao professor uma API alternativa.

---

## Entrega da aula

Para considerar a Aula 08 concluída, entregue:

- link do repositório atualizado;
- print da tela carregando;
- print da lista com usuários;
- print ou descrição do teste de erro;
- resposta curta explicando o que o `fromJson` faz.

Use a página da atividade:

- [Atividade 08 - REST Parte 1 (GET + Lista)](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-08)
- [Formulário Aula 08](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-08)

---

## Materiais relacionados

- [Material 04 - Consumo de APIs REST](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-04)
- [Aula 04 - UI com Listas + Cards](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/aulas/aula-04)
- [Aula 09 - API REST Parte 2](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/aulas/aula-09)

---

## Checklist final

- [ ] API testada no navegador.
- [ ] Pacote `http` instalado.
- [ ] Permissão de internet adicionada.
- [ ] Modelo `Usuario` criado.
- [ ] Service `ApiService` criado.
- [ ] Tela `UsuariosScreen` criada.
- [ ] `main.dart` apontando para `UsuariosScreen`.
- [ ] Loading funcionando.
- [ ] Lista funcionando.
- [ ] Erro tratado com mensagem e botão.
- [ ] Evidências separadas para envio.

---

**Material elaborado para o curso de PAM2 - 2026**  
Prof. Gustavo Villalta

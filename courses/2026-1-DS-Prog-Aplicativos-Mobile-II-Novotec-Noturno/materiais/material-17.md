---
layout: material
title: "Material 17 - Autenticação e Sessão Local"
category: materiais
---

# Autenticação, Token e Sessão Persistente no Flutter

Este material apoia a Aula 06 de PAM2 e foca no fluxo mais importante da noite:
login, armazenamento local do token e decisão automática da tela inicial.

---

## O que você vai praticar

- simular um login assíncrono;
- receber um token simples;
- salvar a sessão com `shared_preferences`;
- abrir a `HomeScreen` automaticamente quando já houver token;
- remover apenas a chave de autenticação no logout.

---

## Conceito base

Em um app mobile, o fluxo costuma ser:

1. o usuário envia credenciais;
2. a API responde com um token;
3. o app guarda esse token;
4. nas próximas aberturas, o app verifica se o token já existe;
5. se existir, o usuário entra direto na área protegida.

Para a aula de hoje, o login é **mockado**. Isso é intencional: a turma aprende
o fluxo de sessão antes de consumir uma API real nas aulas 08 e 09.

---

## Pacote necessário

```bash
flutter pub add shared_preferences
```

Documentação oficial:

- [Flutter cookbook - Key-value persistence](https://docs.flutter.dev/cookbook/persistence/key-value)
- [Package `shared_preferences`](https://pub.dev/packages/shared_preferences)

---

## Serviço de autenticação simulado

Crie `lib/services/auth_service.dart`:

```dart
class AuthService {
  Future<String?> login(String email, String senha) async {
    await Future.delayed(const Duration(seconds: 2));

    if (email == 'aluno@etec.sp.gov.br' && senha == '123456') {
      return 'sucesso_token_123';
    }

    return null;
  }
}
```

Use esse mock para treinar `async`, `await`, feedback visual e fluxo de sucesso
ou falha.

---

## Salvando a sessão

Adicione o import no topo do arquivo:

```dart
import 'package:shared_preferences/shared_preferences.dart';
```

Depois, crie uma função para persistir o token:

```dart
Future<void> salvarSessao(String token) async {
  final prefs = await SharedPreferences.getInstance();
  await prefs.setString('meu_token_seguro', token);
}
```

---

## Decidindo a tela inicial no `main`

```dart
import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();

  final prefs = await SharedPreferences.getInstance();
  final token = prefs.getString('meu_token_seguro');

  runApp(MyApp(estaLogado: token != null));
}
```

Essa leitura acontece antes do `runApp`, por isso o
`WidgetsFlutterBinding.ensureInitialized()` é necessário.

---

## Logout correto

Para esta aula, prefira remover só a chave da sessão:

```dart
Future<void> logout() async {
  final prefs = await SharedPreferences.getInstance();
  await prefs.remove('meu_token_seguro');
}
```

Evite `prefs.clear()` neste exemplo, porque ele apaga todas as preferências do
app, inclusive dados que não têm relação com autenticação.

---

## Boas práticas para a turma

- Não salvar senha real no armazenamento local.
- Usar token fake na aula e JWT/API real nas próximas aulas.
- Mostrar `CircularProgressIndicator` enquanto o login estiver em andamento.
- Navegar com `pushReplacement` depois do login para impedir retorno indevido à
  tela de login.

---

## Materiais relacionados

- [Aula 06 - Autenticação e Persistência de Sessão](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/aulas/aula-06)
- [Material 05 - Formulários e Validação](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-05)
- [Material 04 - Consumo de APIs REST](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-04)

---

**Última atualização:** 22/04/2026

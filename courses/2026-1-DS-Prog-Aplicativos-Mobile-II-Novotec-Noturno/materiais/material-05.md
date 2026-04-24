---
layout: material
title: "Material 05 - Formulários e Validação no Flutter"
---

# 🧾 Material 05 - Formulários e Validação no Flutter

Este material acompanha a **Aula 05** e foi pensado para ser usado como um
roteiro de apoio durante a prática.

O objetivo é construir uma **tela de cadastro funcional**, com validação básica,
feedback ao usuário e organização visual mínima.

---

## O que você vai aprender

Ao final deste material, você deverá conseguir:

- criar um formulário com vários campos,
- capturar textos digitados pelo usuário,
- validar entradas obrigatórias,
- comparar senha e confirmação de senha,
- mostrar mensagens de erro e sucesso.

---

## O que você vai construir

Você vai criar uma tela com:

- campo de nome,
- campo de e-mail,
- campo de senha,
- campo de confirmar senha,
- botão de cadastro.

---

## Estrutura mínima do projeto

Você pode começar com uma única tela dentro do `main.dart` ou separar depois.

Exemplo de estrutura simples:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: const CadastroScreen(),
    );
  }
}
```

---

## Passo 1 - Criar a tela base

Monte a tela com:

- `Scaffold`
- `AppBar`
- `Padding`
- `SingleChildScrollView`
- `Form`

Exemplo:

```dart
class CadastroScreen extends StatefulWidget {
  const CadastroScreen({super.key});

  @override
  State<CadastroScreen> createState() => _CadastroScreenState();
}

class _CadastroScreenState extends State<CadastroScreen> {
  final _formKey = GlobalKey<FormState>();

  final _nomeController = TextEditingController();
  final _emailController = TextEditingController();
  final _senhaController = TextEditingController();
  final _confirmarSenhaController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Cadastro'),
      ),
      body: SingleChildScrollView(
        padding: const EdgeInsets.all(16),
        child: Form(
          key: _formKey,
          child: Column(
            children: [
              // campos aqui
            ],
          ),
        ),
      ),
    );
  }
}
```

---

## Passo 2 - Criar os campos do formulário

### Campo de nome

```dart
TextFormField(
  controller: _nomeController,
  decoration: const InputDecoration(
    labelText: 'Nome',
    border: OutlineInputBorder(),
  ),
)
```

### Campo de e-mail

```dart
TextFormField(
  controller: _emailController,
  keyboardType: TextInputType.emailAddress,
  decoration: const InputDecoration(
    labelText: 'E-mail',
    border: OutlineInputBorder(),
  ),
)
```

### Campo de senha

```dart
TextFormField(
  controller: _senhaController,
  obscureText: true,
  decoration: const InputDecoration(
    labelText: 'Senha',
    border: OutlineInputBorder(),
  ),
)
```

### Campo de confirmar senha

```dart
TextFormField(
  controller: _confirmarSenhaController,
  obscureText: true,
  decoration: const InputDecoration(
    labelText: 'Confirmar senha',
    border: OutlineInputBorder(),
  ),
)
```

### Dica de organização

Coloque um `SizedBox(height: 16)` entre os campos para melhorar a leitura da
interface.

---

## Passo 3 - Adicionar validação

Agora transforme os campos em campos validados.

### Validação de nome

```dart
validator: (value) {
  if (value == null || value.isEmpty) {
    return 'Digite seu nome';
  }
  return null;
}
```

### Validação de e-mail

```dart
validator: (value) {
  if (value == null || value.isEmpty) {
    return 'Digite seu e-mail';
  }
  if (!value.contains('@')) {
    return 'E-mail inválido';
  }
  return null;
}
```

### Validação de senha

```dart
validator: (value) {
  if (value == null || value.isEmpty) {
    return 'Digite uma senha';
  }
  if (value.length < 6) {
    return 'A senha deve ter pelo menos 6 caracteres';
  }
  return null;
}
```

### Validação de confirmar senha

```dart
validator: (value) {
  if (value == null || value.isEmpty) {
    return 'Confirme sua senha';
  }
  if (value != _senhaController.text) {
    return 'As senhas não coincidem';
  }
  return null;
}
```

---

## Passo 4 - Criar o botão de envio

Depois dos campos, adicione um botão:

```dart
SizedBox(
  width: double.infinity,
  child: ElevatedButton(
    onPressed: _enviarFormulario,
    child: const Text('Cadastrar'),
  ),
)
```

Agora crie o método `_enviarFormulario()`:

```dart
void _enviarFormulario() {
  if (_formKey.currentState!.validate()) {
    ScaffoldMessenger.of(context).showSnackBar(
      const SnackBar(
        content: Text('Cadastro realizado com sucesso!'),
      ),
    );
  }
}
```

---

## Exemplo completo

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      debugShowCheckedModeBanner: false,
      home: CadastroScreen(),
    );
  }
}

class CadastroScreen extends StatefulWidget {
  const CadastroScreen({super.key});

  @override
  State<CadastroScreen> createState() => _CadastroScreenState();
}

class _CadastroScreenState extends State<CadastroScreen> {
  final _formKey = GlobalKey<FormState>();
  final _nomeController = TextEditingController();
  final _emailController = TextEditingController();
  final _senhaController = TextEditingController();
  final _confirmarSenhaController = TextEditingController();

  void _enviarFormulario() {
    if (_formKey.currentState!.validate()) {
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(
          content: Text('Cadastro realizado com sucesso!'),
        ),
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Cadastro')),
      body: SingleChildScrollView(
        padding: const EdgeInsets.all(16),
        child: Form(
          key: _formKey,
          child: Column(
            children: [
              TextFormField(
                controller: _nomeController,
                decoration: const InputDecoration(
                  labelText: 'Nome',
                  border: OutlineInputBorder(),
                ),
                validator: (value) {
                  if (value == null || value.isEmpty) {
                    return 'Digite seu nome';
                  }
                  return null;
                },
              ),
              const SizedBox(height: 16),
              TextFormField(
                controller: _emailController,
                keyboardType: TextInputType.emailAddress,
                decoration: const InputDecoration(
                  labelText: 'E-mail',
                  border: OutlineInputBorder(),
                ),
                validator: (value) {
                  if (value == null || value.isEmpty) {
                    return 'Digite seu e-mail';
                  }
                  if (!value.contains('@')) {
                    return 'E-mail inválido';
                  }
                  return null;
                },
              ),
              const SizedBox(height: 16),
              TextFormField(
                controller: _senhaController,
                obscureText: true,
                decoration: const InputDecoration(
                  labelText: 'Senha',
                  border: OutlineInputBorder(),
                ),
                validator: (value) {
                  if (value == null || value.isEmpty) {
                    return 'Digite uma senha';
                  }
                  if (value.length < 6) {
                    return 'A senha deve ter pelo menos 6 caracteres';
                  }
                  return null;
                },
              ),
              const SizedBox(height: 16),
              TextFormField(
                controller: _confirmarSenhaController,
                obscureText: true,
                decoration: const InputDecoration(
                  labelText: 'Confirmar senha',
                  border: OutlineInputBorder(),
                ),
                validator: (value) {
                  if (value == null || value.isEmpty) {
                    return 'Confirme sua senha';
                  }
                  if (value != _senhaController.text) {
                    return 'As senhas não coincidem';
                  }
                  return null;
                },
              ),
              const SizedBox(height: 20),
              SizedBox(
                width: double.infinity,
                child: ElevatedButton(
                  onPressed: _enviarFormulario,
                  child: const Text('Cadastrar'),
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }

  @override
  void dispose() {
    _nomeController.dispose();
    _emailController.dispose();
    _senhaController.dispose();
    _confirmarSenhaController.dispose();
    super.dispose();
  }
}
```

---

## Checklist do aluno

Antes de considerar a atividade pronta, verifique:

- [ ] Existe campo de nome.
- [ ] Existe campo de e-mail.
- [ ] Existe campo de senha.
- [ ] Existe campo de confirmar senha.
- [ ] O formulário valida campos vazios.
- [ ] O e-mail verifica `@`.
- [ ] A senha tem pelo menos 6 caracteres.
- [ ] A confirmação de senha funciona.
- [ ] O botão mostra sucesso quando tudo está correto.

---

## Erros comuns

### 1. O botão não faz nada

Verifique se o botão chama `_enviarFormulario()`.

### 2. O formulário não valida

Confira se o `Form` está com:

```dart
key: _formKey
```

### 3. O app quebra quando o teclado aparece

Use `SingleChildScrollView`.

### 4. A senha e a confirmação nunca batem

Confira se você comparou com `_senhaController.text`.

### 5. Está usando `TextField` em vez de `TextFormField`

Se quiser usar `validator`, o correto é `TextFormField`.

---

## Entrega da aula

Você deve entregar:

- print da tela funcionando,
- evidência de erro de validação,
- evidência de sucesso no envio,
- link do projeto ou repositório.

---

## Para ir além

Se terminar antes, você pode melhorar o app com:

- ícones nos campos,
- botão de mostrar/ocultar senha,
- limpeza automática dos campos após envio,
- layout mais bonito.

---

## Relação com as próximas aulas

Esta aula prepara a base para os próximos passos do curso, quando você vai
trabalhar com:

- login,
- autenticação,
- fluxo entre telas,
- integração com serviços externos.

Hoje, o mais importante é dominar **entrada de dados e validação**.

---

**Material elaborado para Mobile II - 2026**  
Prof. Gustavo Villalta

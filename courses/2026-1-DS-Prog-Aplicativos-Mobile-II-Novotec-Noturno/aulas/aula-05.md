---
layout: aula
title: "Aula 05 - Formulários e Validação (Base para Login e Cadastro)"
course_id: mobile2
category: aulas
---

## Data e contexto

- **Data:** 15/04/2026
- **Duração:** 5 horas-aula
- **Horário real:** 18h45 às 22h20
- **Intervalo sugerido:** 20h25 às 20h40
- **Laboratório:** 6

## Alinhamento com o PTD

- **Habilidades:** 1.1, 1.3, 1.4
- **Bases:** Formulários e validação; entrada de dados; usabilidade básica;
  preparação para fluxo de login e cadastro.

---

## Objetivo da noite

Ao final da aula, a turma deve conseguir construir uma tela de cadastro simples
em Flutter com:

- campos de texto organizados,
- captura de dados com controller,
- validações básicas,
- botão de envio,
- feedback visual para erro e sucesso.

O foco da aula é **formulário funcional e compreensível**. Não é necessário
entrar fundo em backend ou autenticação real nesta etapa.

---

## O que você vai construir hoje

Nesta aula, você vai desenvolver uma **tela de cadastro** com os seguintes
campos:

- nome,
- e-mail,
- senha,
- confirmar senha.

No final, seu app deve:

- impedir envio quando houver campo inválido,
- mostrar mensagens de erro abaixo dos campos,
- exibir uma mensagem de sucesso quando tudo estiver correto.

---

## Resultado esperado

Ao final da aula, seu app deve ter:

- uma tela com `AppBar`,
- um formulário com 4 campos,
- botão de cadastro,
- validação em todos os campos,
- comparação entre senha e confirmação,
- `SnackBar` de sucesso.

---

## Mapa rápido da aula

Siga a aula nesta ordem. Não pule etapas.

1. Criar a tela base com `Scaffold` e `AppBar`.
2. Colocar um `Form` dentro da tela.
3. Criar a chave do formulário (`GlobalKey<FormState>`).
4. Criar os controllers dos campos.
5. Adicionar um campo por vez com `TextFormField`.
6. Testar se a tela abre.
7. Adicionar validação nos campos.
8. Criar o botão `Cadastrar`.
9. Mostrar o `SnackBar` quando o formulário estiver correto.
10. Registrar a evidência da atividade.

Se algo quebrar, volte para o último passo que funcionava.

---

## Documentação oficial que será usada hoje

Use estes links como consulta durante a aula:

- [Flutter - Build a form with validation](https://docs.flutter.dev/cookbook/forms/validation)
- [`Form`](https://api.flutter.dev/flutter/widgets/Form-class.html)
- [`TextFormField`](https://api.flutter.dev/flutter/material/TextFormField-class.html)
- [`TextEditingController`](https://api.flutter.dev/flutter/widgets/TextEditingController-class.html)
- [`Scaffold`](https://api.flutter.dev/flutter/material/Scaffold-class.html)
- [`AppBar`](https://api.flutter.dev/flutter/material/AppBar-class.html)
- [`SingleChildScrollView`](https://api.flutter.dev/flutter/widgets/SingleChildScrollView-class.html)
- [`InputDecoration`](https://api.flutter.dev/flutter/material/InputDecoration-class.html)
- [`TextInputType.emailAddress`](https://api.flutter.dev/flutter/services/TextInputType/emailAddress-constant.html)
- [`ElevatedButton`](https://api.flutter.dev/flutter/material/ElevatedButton-class.html)
- [`ScaffoldMessenger`](https://api.flutter.dev/flutter/material/ScaffoldMessenger-class.html)
- [`SnackBar`](https://api.flutter.dev/flutter/material/SnackBar-class.html)

---

## Organização da aula

### Bloco 1, 18h45 às 19h35

## 1. Preparação e primeira tela funcionando

### Passo 1. Abra o projeto

Abra o projeto Flutter usado nas aulas anteriores. Se preferir começar limpo,
crie um projeto novo e trabalhe no arquivo `lib/main.dart`.

Antes de codar, rode o app uma vez para confirmar que o ambiente está
funcionando.

### Passo 2. Crie a base da tela

Monte uma tela simples usando:

- `Scaffold`,
- `AppBar`,
- `SingleChildScrollView`,
- `Padding`,
- `Column`.

Referências oficiais:

- [`Scaffold`](https://api.flutter.dev/flutter/material/Scaffold-class.html)
- [`AppBar`](https://api.flutter.dev/flutter/material/AppBar-class.html)
- [`SingleChildScrollView`](https://api.flutter.dev/flutter/widgets/SingleChildScrollView-class.html)

Estrutura inicial:

```dart
class CadastroScreen extends StatefulWidget {
  const CadastroScreen({super.key});

  @override
  State<CadastroScreen> createState() => _CadastroScreenState();
}

class _CadastroScreenState extends State<CadastroScreen> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Cadastro')),
      body: SingleChildScrollView(
        padding: const EdgeInsets.all(16),
        child: Column(
          children: const [
            Text('Tela de cadastro'),
          ],
        ),
      ),
    );
  }
}
```

### Checkpoint 1

Antes de continuar, confirme:

- [ ] O app abre.
- [ ] A tela mostra o título `Cadastro`.
- [ ] Não existe erro vermelho no console.

### Passo 3. Coloque o `Form`

O `Form` é o widget que agrupa os campos e permite validar tudo de uma vez.

Referência oficial:

- [`Form`](https://api.flutter.dev/flutter/widgets/Form-class.html)

Crie a chave do formulário dentro do `_CadastroScreenState`:

```dart
final _formKey = GlobalKey<FormState>();
```

Depois, coloque o `Form` dentro do `SingleChildScrollView`:

```dart
body: SingleChildScrollView(
  padding: const EdgeInsets.all(16),
  child: Form(
    key: _formKey,
    child: Column(
      children: const [
        Text('Campos do formulário aqui'),
      ],
    ),
  ),
),
```

### Passo 4. Crie os controllers

Crie controllers para capturar os valores digitados:

```dart
final _nomeController = TextEditingController();
final _emailController = TextEditingController();
final _senhaController = TextEditingController();
final _confirmarSenhaController = TextEditingController();
```

Referência oficial:

- [`TextEditingController`](https://api.flutter.dev/flutter/widgets/TextEditingController-class.html)

### Atenção

Se você esquecer de colocar `key: _formKey` dentro do `Form`, a validação não
vai funcionar corretamente.

---

### Bloco 2, 19h35 às 20h25

## 2. Montagem dos campos do formulário

Agora monte os quatro campos com `TextFormField`.

Referências oficiais:

- [`TextFormField`](https://api.flutter.dev/flutter/material/TextFormField-class.html)
- [`InputDecoration`](https://api.flutter.dev/flutter/material/InputDecoration-class.html)
- [`TextInputType.emailAddress`](https://api.flutter.dev/flutter/services/TextInputType/emailAddress-constant.html)

### Passo 1. Comece por apenas um campo

Primeiro crie o campo de nome e rode o app.

```dart
TextFormField(
  controller: _nomeController,
  decoration: const InputDecoration(
    labelText: 'Nome',
    border: OutlineInputBorder(),
  ),
)
```

Se esse campo apareceu corretamente, continue.

### Campo 1. Nome

Use um campo simples de texto com `labelText: 'Nome'`.

### Campo 2. E-mail

Use teclado apropriado para e-mail:

```dart
keyboardType: TextInputType.emailAddress,
```

### Campo 3. Senha

Use:

```dart
obscureText: true,
```

### Campo 4. Confirmar senha

Também deve usar `obscureText: true`.

### Passo 2. Use o mesmo padrão nos quatro campos

Para cada campo, mantenha:

- `controller`,
- `decoration`,
- `labelText`,
- `border: OutlineInputBorder()`.

Entre um campo e outro, use:

```dart
const SizedBox(height: 16)
```

### Dicas visuais

Em cada campo, adicione pelo menos:

- `labelText`,
- borda (`OutlineInputBorder`),
- espaçamento entre os campos.

### Checkpoint 2

Antes do intervalo, o mínimo esperado é:

- [ ] A tela mostra os quatro campos.
- [ ] Os campos aceitam digitação.
- [ ] A senha fica escondida.
- [ ] A tela não quebra quando o teclado abre.

Se a tela quebrar com o teclado, confira se o conteúdo está dentro de
`SingleChildScrollView`.

---

### Intervalo, 20h25 às 20h40

Meta ideal antes do intervalo: deixar o formulário montado visualmente, mesmo
que ainda sem todas as regras de validação.

---

### Bloco 3, 20h40 às 21h30

## 3. Validação dos campos

Agora você vai fazer o formulário verificar se os dados estão corretos.

Referência oficial:

- [Flutter - Build a form with validation](https://docs.flutter.dev/cookbook/forms/validation)

### Como o `validator` funciona

Cada `TextFormField` pode ter um `validator`.

- Se tiver erro, o `validator` retorna uma mensagem de texto.
- Se estiver correto, o `validator` retorna `null`.

Exemplo:

```dart
validator: (value) {
  if (value == null || value.isEmpty) {
    return 'Digite seu nome';
  }
  return null;
},
```

### Regra 1. Campo obrigatório

Exemplo:

```dart
validator: (value) {
  if (value == null || value.isEmpty) {
    return 'Campo obrigatório';
  }
  return null;
}
```

### Regra 2. E-mail simples

Você pode começar com uma validação simples:

```dart
if (value == null || value.isEmpty) {
  return 'Digite seu e-mail';
}
if (!value.contains('@')) {
  return 'E-mail inválido';
}
return null;
```

### Regra 3. Senha mínima

Exemplo:

```dart
if (value == null || value.isEmpty) {
  return 'Digite uma senha';
}
if (value.length < 6) {
  return 'A senha deve ter pelo menos 6 caracteres';
}
return null;
```

### Regra 4. Confirmar senha

O campo de confirmação deve comparar com a senha original:

```dart
if (value != _senhaController.text) {
  return 'As senhas não coincidem';
}
return null;
```

### O que evitar

Não tente fazer validações avançadas demais nesta aula. O importante hoje é
entender o fluxo básico.

### Checkpoint 3

Teste estes casos antes de seguir:

- [ ] Clicar em cadastrar com tudo vazio mostra erros.
- [ ] E-mail sem `@` mostra erro.
- [ ] Senha com menos de 6 caracteres mostra erro.
- [ ] Senhas diferentes mostram erro.
- [ ] Dados corretos não mostram erro nos campos.

---

### Bloco 4, 21h30 às 22h10

## 4. Botão de envio e feedback

Agora crie o botão final do formulário.

Referências oficiais:

- [`ElevatedButton`](https://api.flutter.dev/flutter/material/ElevatedButton-class.html)
- [`ScaffoldMessenger`](https://api.flutter.dev/flutter/material/ScaffoldMessenger-class.html)
- [`SnackBar`](https://api.flutter.dev/flutter/material/SnackBar-class.html)

### Passo 1. Crie o método de envio

```dart
void _enviarFormulario() {
  if (_formKey.currentState!.validate()) {
    ScaffoldMessenger.of(context).showSnackBar(
      const SnackBar(content: Text('Cadastro realizado com sucesso!')),
    );
  }
}
```

### Passo 2. Associe o método ao botão

```dart
SizedBox(
  width: double.infinity,
  child: ElevatedButton(
    onPressed: _enviarFormulario,
    child: const Text('Cadastrar'),
  ),
)
```

### Passo 3. Entenda a lógica

Esta linha pergunta ao formulário se todos os campos estão corretos:

```dart
_formKey.currentState!.validate()
```

Se a resposta for `true`, o app mostra uma mensagem de sucesso:

```dart
ScaffoldMessenger.of(context).showSnackBar(
  const SnackBar(content: Text('Cadastro realizado com sucesso!')),
);
```

### Desafio final da aula

Seu app deve conseguir:

- validar todos os campos,
- impedir envio quando houver erro,
- mostrar mensagem de sucesso quando tudo estiver correto.

### Se terminar antes

Se você concluir cedo, pode melhorar:

- ícones nos campos,
- botão mais bonito,
- limpeza automática do formulário,
- botão desabilitado durante envio.

---

### Fechamento, 22h10 às 22h20

## 5. Entrega da aula

Antes de encerrar, confira se seu projeto atende ao mínimo.

### Checklist de conclusão

- [ ] A tela abre sem erro.
- [ ] O formulário possui nome, e-mail, senha e confirmar senha.
- [ ] Todos os campos têm validação.
- [ ] A confirmação de senha funciona.
- [ ] O botão executa a validação.
- [ ] Existe feedback visual de sucesso.

### O que entregar

Você deve registrar:

- print da tela funcionando,
- print ou vídeo curto mostrando a validação,
- link do projeto ou repositório,
- resposta curta sobre a maior dificuldade da aula.

---

## Atividade integrada da aula

A atividade desta noite já está dentro deste roteiro.

### Sua missão

Criar uma **tela de cadastro funcional** com:

- nome,
- e-mail,
- senha,
- confirmação de senha,
- validações,
- feedback de sucesso.

### Critério mínimo para considerar concluído

Seu app precisa ter:

- interface organizada,
- validação funcionando,
- botão de envio,
- mensagem de erro e de sucesso.

### Critérios de avaliação

- **4 pts**: interface montada e sem erros graves.
- **4 pts**: validações funcionando corretamente.
- **2 pts**: organização, clareza do código e qualidade da entrega.

---

## Estrutura do formulário (Google Forms)

| Ordem | Pergunta                                                   | Tipo de resposta | Observação técnica       |
| :---- | :--------------------------------------------------------- | :--------------- | :----------------------- |
| 1     | Nome completo                                              | Resposta curta   | Identificação            |
| 2     | Seu formulário valida campos obrigatórios?                 | Múltipla escolha | Sim / Parcialmente / Não |
| 3     | Qual widget usamos para validar vários campos em conjunto? | Múltipla escolha | `Form`                   |
| 4     | O que o `validator` retorna quando o campo está correto?   | Múltipla escolha | `null`                   |
| 5     | Link do projeto ou print da tela funcionando               | Resposta curta   | Evidência                |
| 6     | Qual foi sua maior dificuldade na aula?                    | Parágrafo        | Diagnóstico              |

---

## Dicas de ouro para a aula noturna

1. **Comece com resultado visível rápido**: o aluno precisa ver a tela
   aparecendo cedo para não perder o ritmo.
2. **Quebre a explicação em blocos pequenos**: longas sequências de teoria às
   21h costumam derrubar a atenção.
3. **Use validação simples primeiro**: deixe regex e refinamentos mais avançados
   para uma aula futura, se necessário.
4. **Teste no aparelho ou emulador com teclado aberto**: isso gera discussões
   reais sobre overflow e usabilidade.
5. **Feche com sensação de entrega**: mesmo que nem todos terminem completo,
   vale garantir que saiam com uma versão funcional mínima.

## Apoio rápido para copiar e adaptar

Se você travar, use esta estrutura como referência inicial:

```dart
final _formKey = GlobalKey<FormState>();
final _nomeController = TextEditingController();
final _emailController = TextEditingController();
final _senhaController = TextEditingController();
final _confirmarSenhaController = TextEditingController();

void _enviarFormulario() {
  if (_formKey.currentState!.validate()) {
    ScaffoldMessenger.of(context).showSnackBar(
      const SnackBar(content: Text('Cadastro realizado com sucesso!')),
    );
  }
}
```

Exemplo de campo com validação:

```dart
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
)
```

---

## Se algo der errado

### O botão não valida

Verifique se:

- o `Form` tem `key: _formKey`,
- o botão chama `_formKey.currentState!.validate()`.

### A mensagem de erro não aparece

Verifique se o campo foi criado com `TextFormField` e não com `TextField`.

### A tela quebra quando o teclado abre

Use `SingleChildScrollView`.

### A confirmação de senha não funciona

Confira se você comparou com `_senhaController.text`.

---

## Materiais relacionados

- [Material 05 - Formulários e Validação no Flutter](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-05)
- [Atividade 04 - Formulário de Cadastro](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-04)
- [Página de atividades](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/)

---

**Material elaborado para o curso de PAM2 - 2026**  
Prof. Gustavo Villalta

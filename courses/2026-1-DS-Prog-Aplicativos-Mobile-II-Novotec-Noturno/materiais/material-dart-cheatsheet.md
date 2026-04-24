---
layout: material
title: "Dart Cheat Sheet - Referência Rápida"
---

# 📋 Dart Cheat Sheet - Referência Rápida para Flutter

> **Guia de bolso para consultas rápidas durante o curso PAM2**  
> **Foco:** Sintaxe essencial para quem está começando com Flutter

---

## 📦 1. Variáveis e Tipos

### Declaração Básica

```dart
// Inferência de tipos (Dart adivinha)
var nome = "Gustavo";     // String
var idade = 30;           // int
var altura = 1.75;        // double
var estudante = true;     // bool

// Tipos explícitos (mais seguro)
String sobrenome = "Villalta";
int quantidade = 10;
double preco = 29.90;
bool ativo = false;

// Dinâmico (evite usar!)
dynamic qualquer = "texto";
qualquer = 123;  // Funciona, mas não recomendado
```

### Null Safety (MUITO IMPORTANTE!)

```dart
// NÃO pode ser null (padrão)
String nome = "Maria";
// nome = null;  // ❌ ERRO de compilação!

// PODE ser null (usa ?)
String? telefone = null;
telefone = "19999999999";  // ✅ OK

// Como usar variável nullable:
// 1. Operador ?? (valor padrão se for null)
String telefoneOuPadrao = telefone ?? "Não informado";

// 2. Operador ?. (acessa só se não for null)
int? tamanho = telefone?.length;  // null se telefone for null

// 3. Operador ! (força não-null - use com cuidado!)
int tamanhoSeguro = telefone!.length;  // ❌ CRASH se for null!

// 4. if-let (verifica e usa)
if (telefone != null) {
  print(telefone.length);  // ✅ Seguro
}
```

---

## 🔧 2. Funções

### Sintaxe Básica

```dart
// Função tradicional
int somar(int a, int b) {
  return a + b;
}

// Arrow function (função de uma linha)
int somarArrow(int a, int b) => a + b;

// Função sem retorno (void)
void saudar(String nome) {
  print('Olá, $nome!');
}

// Parâmetros opcionais (entre colchetes)
String saudarOpcional(String nome, [String? saudacao]) {
  return '$saudacao, $nome!';
}
saudarOpcional("Maria");           // "null, Maria!"
saudarOpcional("Maria", "Oi");     // "Oi, Maria!"
```

### Parâmetros Nomeados (ESTILO FLUTTER!)

```dart
// Usado em TODOS os widgets do Flutter!
void criarPerfil({
  required String nome,      // OBRIGATÓRIO
  required int idade,        // OBRIGATÓRIO
  String? cidade,            // Opcional + nullable
  String pais = "Brasil",    // Opcional com valor padrão
}) {
  print('$nome, $idade anos, de $cidade - $pais');
}

// Chamadas (ordem NÃO importa!):
criarPerfil(nome: "João", idade: 20);
criarPerfil(idade: 25, nome: "Ana", cidade: "São Paulo");
criarPerfil(nome: "Pedro", idade: 30, pais: "Portugal");
```

---

## 🏗️ 3. Classes e Objetos (POO)

### Classe Básica

```dart
class Pessoa {
  // Atributos
  String nome;
  int idade;

  // Construtor tradicional
  Pessoa(this.nome, this.idade);

  // Método
  void apresentar() {
    print('Olá, sou $nome e tenho $idade anos');
  }
}

// Uso:
var p = Pessoa("Maria", 25);
p.apresentar();  // "Olá, sou Maria e tenho 25 anos"
```

### Construtores Nomeados (MUITO USADO NO FLUTTER!)

```dart
class Pessoa {
  String nome;
  int idade;
  String? cidade;

  // Construtor nomeado
  Pessoa.anonima()
    : nome = "Anônimo",
      idade = 0,
      cidade = null;

  // Construtor com parâmetros nomeados (padrão Flutter!)
  Pessoa.completa({
    required this.nome,
    required this.idade,
    this.cidade,  // opcional (é nullable)
  });

  // Construtor a partir de JSON (para APIs!)
  Pessoa.fromJson(Map<String, dynamic> json)
    : nome = json['nome'],
      idade = json['idade'],
      cidade = json['cidade'];
}

// Uso:
var p1 = Pessoa.anonima();
var p2 = Pessoa.completa(nome: "Ana", idade: 20, cidade: "Campinas");
var p3 = Pessoa.completa(idade: 30, nome: "Pedro");  // ordem não importa!

// JSON (muito usado com APIs):
var json = {'nome': 'Carlos', 'idade': 25, 'cidade': 'São Paulo'};
var p4 = Pessoa.fromJson(json);
```

---

## 📊 4. Coleções

### Listas (Arrays)

```dart
// Declaração
List<String> nomes = ['Ana', 'Bruno', 'Carla'];
var numeros = [1, 2, 3, 4, 5];  // com inferência

// Operações comuns
nomes.add("Daniel");           // Adiciona
nomes.remove("Ana");           // Remove
nomes.length;                  // Tamanho: 3
nomes[0];                      // Primeiro elemento: "Bruno"

// Loop com for-in
for (var nome in nomes) {
  print(nome);
}

// Métodos úteis
nomes.forEach((n) => print(n));           // Para cada
var maiusculas = nomes.map((n) => n.toUpperCase()).toList();
var filtrados = nomes.where((n) => n.length > 4).toList();
```

### Mapas (Dicionários)

```dart
// Declaração
Map<String, dynamic> produto = {
  'nome': 'Notebook',
  'preco': 3500.0,
  'estoque': 10,
};

// Acesso
produto['nome'];        // 'Notebook'
produto['preco'] = 3200.0;  // Atualiza

// Loop
produto.forEach((chave, valor) {
  print('$chave: $valor');
});

// JSON é um Mapa!
var usuario = {
  'id': 1,
  'nome': 'Maria',
  'email': 'maria@etec.sp.gov.br',
};
```

---

## ⏱️ 5. Async/Await (CRÍTICO!)

### Conceitos Fundamentais

```dart
// Future = "valor que vai chegar no futuro"
// async = "essa função demora para completar"
// await = "espera isso terminar antes de continuar"

// Exemplo básico:
Future<String> buscarDados() async {
  // Simula operação demorada (API, banco de dados, etc.)
  await Future.delayed(Duration(seconds: 2));
  return "Dados carregados!";
}

void main() async {
  print("Iniciando...");

  var dados = await buscarDados();  // ⏳ ESPERA 2 segundos
  print(dados);  // "Dados carregados!"

  print("Fim!");
}
```

### Try-Catch com Async

```dart
Future<void> buscarUsuario() async {
  try {
    var response = await http.get('https://api.exemplo.com/usuario');
    print('Usuário: ${response.body}');
  } catch (erro) {
    print('Erro ao buscar: $erro');
  } finally {
    print('Operação concluída');
  }
}
```

### Analogia do Delivery 🍕

```dart
// Sem async/await (caótico):
pedirPizza();
assistirTV();  // Começa antes da pizza chegar?
comerPizza();  // Come antes de chegar?

// Com async/await (organizado):
await pedirPizza();      // Pede e ESPERA chegar
assistirTV();            // Só assiste DEPOIS que pizza chegou
await comerPizza();      // Come a pizza (óbvio!)
```

---

## 🎯 6. Estruturas de Controle

### If-Else

```dart
int idade = 17;

if (idade >= 18) {
  print("Maior de idade");
} else if (idade == 17) {
  print("Quase lá...");
} else {
  print("Menor de idade");
}

// If ternário
String status = idade >= 18 ? "Maior" : "Menor";

// Operador ?? (null coalescing)
String? nome = null;
String nomeFinal = nome ?? "Anônimo";  // "Anônimo"
```

### Switch-Case

```dart
String dia = "SEG";

switch (dia) {
  case "SEG":
    print("Segunda-feira");
    break;
  case "TER":
    print("Terça-feira");
    break;
  default:
    print("Outro dia");
}
```

---

## 🔄 7. Loops

### For Tradicional

```dart
for (int i = 0; i < 5; i++) {
  print(i);  // 0, 1, 2, 3, 4
}
```

### For-In (Mais comum em Flutter)

```dart
var nomes = ['Ana', 'Bruno', 'Carla'];

for (var nome in nomes) {
  print(nome);
}

// Com índice (se precisar)
nomes.asMap().forEach((indice, nome) {
  print('$indice: $nome');
});
```

### While e Do-While

```dart
int i = 0;
while (i < 5) {
  print(i);
  i++;
}

int j = 0;
do {
  print(j);
  j++;
} while (j < 5);
```

---

## 🎨 8. O Que Você Vê no Flutter

### Padrão de Widget Típico

```dart
import 'package:flutter/material.dart';

// Widget stateless (sem estado mutável)
class MinhaTela extends StatelessWidget {
  const MinhaTela({super.key});  // Construtor com key

  @override
  Widget build(BuildContext context) {
    // Método que "desenha" a tela
    return Scaffold(
      appBar: AppBar(
        title: const Text('Título'),
      ),
      body: const Center(
        child: Text('Conteúdo'),
      ),
    );
  }
}

// Widget stateful (com estado mutável)
class Contador extends StatefulWidget {
  const Contador({super.key});

  @override
  State<Contador> createState() => _ContadorState();
}

class _ContadorState extends State<Contador> {
  int _contador = 0;  // Estado privado

  void _incrementar() {
    setState(() {  // AVISA o Flutter que algo mudou!
      _contador++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Text('Contador: $_contador');
  }
}
```

---

## 📝 9. Glossário Rápido

| Termo         | Significado                      | Exemplo                         |
| ------------- | -------------------------------- | ------------------------------- |
| `var`         | Inferência de tipo               | `var x = 10;`                   |
| `final`       | Imutável (runtime)               | `final agora = DateTime.now();` |
| `const`       | Imutável (compile-time)          | `const pi = 3.14;`              |
| `?`           | Nullable (pode ser null)         | `String? nome;`                 |
| `!`           | Null assertion (força não-null)  | `nome!.length;`                 |
| `??`          | Null coalescing (valor padrão)   | `nome ?? "Anônimo"`             |
| `?.`          | Null-aware access                | `nome?.length;`                 |
| `=>`          | Arrow function                   | `int soma() => a + b;`          |
| `required`    | Parâmetro obrigatório            | `required this.nome;`           |
| `@override`   | Sobrescreve método da classe pai | `@override Widget build(...) {` |
| `Future<T>`   | Valor que chega no futuro        | `Future<String>`                |
| `async/await` | Programação assíncrona           | `await http.get();`             |

---

## 🔗 10. Links Úteis

- **DartPad (testar código online):** https://dartpad.dev
- **Documentação Oficial:** https://dart.dev/guides
- **Tour pela linguagem:** https://dart.dev/guides/language/language-tour
- **Null Safety em detalhes:** https://dart.dev/null-safety
- **Async/Await tutorial:** https://dart.dev/codelabs/async-await

---

## 💡 Dicas de Estudo

1. **Não decore sintaxe** - entenda o conceito e consulte este guia
2. **Pratique no DartPad** - teste cada exemplo
3. **Foque em:** Null Safety, Parâmetros Nomeados, Async/Await
4. **Volte aqui sempre** - é normal consultar durante o curso
5. **Anote suas dúvidas** - pergunte ao professor na aula

---

**Material de apoio para o curso PAM2 - 2026**  
Prof. Gustavo Villalta  
ETEC Ferrucio Humberto Gazzetta - Nova Odessa/SP

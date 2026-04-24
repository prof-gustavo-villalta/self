---
layout: aula
title: "Aula 02 - Dart Essencial + Estrutura Flutter + Hello World no Celular"
course_id: mobile2
category: aulas
---

## Data e contexto

- **Data planejada:** 25/03/2026
- **Duração:** 5 horas-aula (250 min)
- **Horário:** 18h45 às 23h10 (considerando 15 min de intervalo)
- **Laboratório:** 6
- **Objetivo da aula:** consolidar o setup, dominar a sintaxe essencial de Dart
  e sair da aula com um app Flutter rodando em hardware real ou emulador.

## Alinhamento com o PTD

- **Habilidades:** 1.1, 1.2
- **Bases:** configuração do ambiente; estrutura do projeto; organização do
  fluxo de trabalho; prática assistida em laboratório.

---

## Resultado esperado ao final da aula

Ao final desta aula, o aluno deve conseguir:

- Executar `flutter doctor` e identificar problemas principais do ambiente.
- Conectar um celular Android ou iniciar um emulador.
- Entender `var`, `final`, `const`, tipos básicos, `?`, `??`, classes,
  construtores nomeados e `async/await`.
- Criar um projeto com `flutter create`.
- Abrir, editar e executar o app padrão no Flutter.
- Fazer uma alteração simples e validar o Hot Reload.

---

## Preparação antes de começar

### O que o aluno precisa ter

- VS Code com extensões **Flutter** e **Dart**.
- Flutter instalado e acessível no terminal.
- Android Studio instalado ou celular Android com cabo USB de dados.
- Pasta para salvar o projeto da aula.

### Materiais de apoio desta aula

- [Material 01 - Guia de Instalação Flutter](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-01)
- [Material 03 - Guia de Instalação Portátil](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-03)
- [Dart Cheat Sheet](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-dart-cheatsheet)
- [Atividade 02 - Dart Speedrun](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-02)
- [Formulário Aula 02](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-02)

---

## Roteiro da aula para seguir sozinho

## 1. Triagem rápida do ambiente (30 min)

Abra o terminal e execute:

```bash
flutter doctor
```

### Você deve observar

- Se o **Flutter** aparece com check verde.
- Se o **Android toolchain** está configurado.
- Se o **VS Code** foi detectado.
- Se existe ao menos um dispositivo disponível depois, em `flutter devices`.

### Se aparecer erro

- **Licenças Android pendentes:** execute `flutter doctor --android-licenses` e
  responda `y`.
- **Celular não reconhecido:** teste outro cabo, outra porta USB e confirme a
  depuração USB no aparelho.
- **Flutter não reconhecido no terminal:** revise o `Path` usando o
  [Material 01](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-01)
  ou o
  [Material 03](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-03).

### Comando complementar

```bash
flutter devices
```

Se aparecer um dispositivo, você já está pronto para rodar o app.

---

## 2. Dart essencial I: sintaxe mínima para sobreviver no Flutter (45 min)

Estude e teste os conceitos abaixo no **DartPad** ou no VS Code.

### Variáveis e tipos

```dart
void main() {
  var nome = 'Ana';
  int idade = 17;
  double altura = 1.65;
  bool estudaMobile = true;

  print('$nome tem $idade anos, mede $altura m e estuda mobile? $estudaMobile');
}
```

### `var`, `final` e `const`

- `var`: a variável recebe um tipo inferido.
- `final`: valor definido uma vez em tempo de execução.
- `const`: valor constante conhecido em tempo de compilação.

```dart
final hoje = DateTime.now();
const escola = 'ETEC';
```

### Null Safety

```dart
void main() {
  String? apelido;

  print(apelido ?? 'Sem apelido');
}
```

### O que você precisa guardar

- `String` não aceita `null` por padrão.
- `String?` aceita `null`.
- `??` define um valor padrão se vier `null`.

---

## 3. Dart essencial II: funções, classes e async (45 min)

### Função com parâmetros nomeados

```dart
void criarPerfil({
  required String nome,
  required int idade,
  String cidade = 'Não informada',
}) {
  print('$nome, $idade anos, cidade: $cidade');
}
```

### Classe simples com construtor nomeado

```dart
class Usuario {
  String nome;
  int idade;

  Usuario({required this.nome, required this.idade});
}

void main() {
  var aluno = Usuario(nome: 'Bruno', idade: 18);
  print(aluno.nome);
}
```

### `Future`, `async` e `await`

```dart
Future<String> carregarMensagem() async {
  await Future.delayed(Duration(seconds: 2));
  return 'Dados carregados';
}

void main() async {
  print('Início');
  var mensagem = await carregarMensagem();
  print(mensagem);
}
```

### O que você precisa guardar

- Flutter usa **parâmetros nomeados** em quase tudo.
- `required` obriga o preenchimento do parâmetro.
- `await` faz sentido quando algo demora, como API, banco ou arquivo.

---

## 4. Criando o primeiro projeto Flutter da aula (50 min)

No terminal, navegue até sua pasta de estudos e execute:

```bash
flutter create --org br.com.etec aula02_hello_mobile
```

Depois entre na pasta:

```bash
cd aula02_hello_mobile
```

Abra no VS Code:

```bash
code .
```

### Arquivos que você deve localizar

- `lib/main.dart`: ponto de entrada do app.
- `pubspec.yaml`: dependências e configurações.

### Leitura guiada do `main.dart`

Procure por estes elementos:

- `void main()`
- `runApp(...)`
- `MaterialApp`
- `Scaffold`
- `AppBar`
- `FloatingActionButton`

### Alteração obrigatória

Troque o título da `AppBar` para algo pessoal, por exemplo:

```dart
appBar: AppBar(
  title: const Text('App do Gustavo'),
),
```

Troque também o texto principal da tela para identificar seu projeto.

---

## 5. Rodando no celular ou emulador (45 min)

Com o dispositivo conectado ou emulador aberto, execute:

```bash
flutter run
```

Se quiser escolher um dispositivo específico:

```bash
flutter run -d <id_do_dispositivo>
```

### O que esperar

- A primeira compilação pode demorar alguns minutos.
- Quando o app abrir, faça uma alteração simples no texto ou na cor.
- Salve com `Ctrl+S` para ver o **Hot Reload**.

### Teste de alteração rápida

Mude, por exemplo:

```dart
home: const MyHomePage(title: 'Meu Primeiro App Flutter'),
```

Depois salve e verifique se a interface atualizou.

---

## 6. Mini checklist de autonomia (15 min)

Antes de encerrar, confirme:

- [ ] Rodei `flutter doctor`.
- [ ] Rodei `flutter devices`.
- [ ] Criei um projeto com `flutter create`.
- [ ] Abri o projeto no VS Code.
- [ ] Identifiquei `main.dart` e `pubspec.yaml`.
- [ ] Rodei o app em emulador ou celular.
- [ ] Fiz uma alteração e validei o Hot Reload.
- [ ] Iniciei a
      [Atividade 02](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-02).

---

## 7. Entrega da aula

Para considerar a aula concluída, o aluno deve apresentar:

- Um print ou foto do app rodando.
- O projeto salvo em pasta pessoal, Drive ou GitHub.
- Pelo menos os exercícios 1 a 4 da
  [Atividade 02](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-02)
  iniciados ou concluídos.
- O
  [Formulário Aula 02](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-02)
  preenchido.

---

## 8. Troubleshooting rápido

### Problema: `flutter` não é reconhecido

- Feche e abra o terminal.
- Revise o `Path`.
- Consulte o
  [Material 01](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-01).

### Problema: celular não aparece

- Ative o modo desenvolvedor.
- Ative a depuração USB.
- Aceite a permissão no celular.
- Troque o cabo USB.

### Problema: app não atualiza

- Salve o arquivo com `Ctrl+S`.
- Veja se o `flutter run` ainda está ativo no terminal.
- Se travar, encerre e rode novamente.

### Problema: erro em `pubspec.yaml`

- YAML é sensível à indentação.
- Use sempre 2 espaços, nunca tabulação.

---

## 9. Guia para o professor

### Foco pedagógico

- Esta aula ainda é de **base**. O objetivo não é produzir interface bonita, mas
  garantir ambiente funcional e vocabulário mínimo de Dart.
- Priorize **execução real do app** acima de explicações muito abstratas.
- Se metade da turma ainda estiver em setup, reduza a profundidade de `async` e
  preserve o tempo do `flutter run`.

### Pontos que mais geram dúvida

- Diferença entre `var`, `final` e `const`.
- `String` versus `String?`.
- Entendimento de parâmetros nomeados.
- Diferença entre compilar pela primeira vez e usar Hot Reload.

### Estratégia de condução

1. Faça a triagem do laboratório primeiro.
2. Resolva bloqueios coletivos em voz alta.
3. Coloque os alunos que finalizaram o setup para apoiar colegas próximos.
4. Feche a aula exigindo evidência de execução.

---

## Estrutura do Formulário (Google Forms)

| Ordem | Pergunta                                                     | Tipo de Resposta | Observação Técnica                  |
| :---- | :----------------------------------------------------------- | :--------------- | :---------------------------------- |
| 1     | Nome Completo                                                | Resposta curta   | Identificação                       |
| 2     | O que significa o operador `?` após um tipo (ex: `String?`)? | Múltipla escolha | Testa Null Safety                   |
| 3     | Qual comando via terminal cria um novo projeto Flutter?      | Múltipla escolha | Resposta esperada: `flutter create` |
| 4     | Qual a diferença entre Hot Reload e Hot Restart?             | Parágrafo curto  | Verifica compreensão operacional    |
| 5     | Link ou print do app rodando no celular ou emulador          | Upload / Link    | Evidência da prática                |

---

## Dicas de ouro para o laboratório noturno

1. **Guerra dos cabos:** tenha cabos de dados reserva.
2. **Rede instável:** mantenha SDK e instaladores em pendrive.
3. **Fadiga após 21h:** faça checkpoints práticos curtos para manter a turma em
   movimento.

## Materiais relacionados

- [Material 01 - Setup Padrão](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-01)
- [Material 03 - Instalação Portátil](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-03)
- [Dart Cheat Sheet](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-dart-cheatsheet)
- [Atividade 02 - Exercícios de Dart](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-02)
- [Formulário Aula 02](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-02)

---

**Material elaborado para o curso de PAM2 - 2026**  
Prof. Gustavo Villalta

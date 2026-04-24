---
layout: aula
title: "Aula 03 - Widgets de Layout + Interatividade (Stateful) + Navegação"
course_id: mobile2
category: aulas
---

## Data e contexto

- **Data planejada:** 01/04/2026
- **Duração:** 5 horas-aula (250 min)
- **Horário:** 18h45 às 23h10 (considerando 15 min de intervalo)
- **Laboratório:** 6
- **Objetivo da aula:** sair do app básico da aula anterior para uma interface
  com organização visual, estado local e navegação entre duas telas.

## Alinhamento com o PTD

- **Habilidades:** 1.1, 1.4
- **Bases:** construção de interfaces; componentes visuais; navegação entre
  telas; organização de layout e usabilidade básica.

---

## Resultado esperado ao final da aula

Ao final desta aula, o aluno deve conseguir:

- Montar uma tela com `Scaffold`, `AppBar`, `Column`, `Row`, `Padding` e
  `SizedBox`.
- Explicar a diferença entre `StatelessWidget` e `StatefulWidget`.
- Atualizar a interface com `setState()`.
- Navegar entre duas telas usando `Navigator.push()` e `Navigator.pop()`.
- Passar um dado simples da tela principal para a tela de detalhes.
- Entregar um app funcional com contador, lista e tela de detalhes.

---

## Preparação antes de começar

### O que o aluno precisa ter

- Flutter funcionando no terminal.
- Projeto da Aula 02 criado ou um novo projeto Flutter limpo.
- VS Code com extensões Flutter e Dart.
- Celular Android ou emulador configurado.

### Materiais de apoio desta aula

- [Material 02 - Slides das Aulas](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-02)
- [Material 16 - Arquitetura Flutter](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-16)
- [Atividade 05 - Interatividade e Navegação (2 Telas)](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-05)
- [Formulário Aula 03](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-03)
- [Documentação oficial de Widgets](https://docs.flutter.dev/ui/widgets)

---

## Roteiro da aula para seguir sozinho

## 1. Revisão rápida da base do app (20 min)

Abra o projeto no terminal:

```bash
flutter devices
flutter run
```

Confirme que o projeto abre sem erro antes de começar a alterar layout e
navegação.

### Checklist rápido

- O app compila.
- O dispositivo está conectado.
- O Hot Reload está funcionando com `Ctrl+S`.

---

## 2. Entendendo a árvore de widgets (35 min)

No Flutter, a tela é uma árvore. Um exemplo simples:

```dart
Scaffold(
  appBar: AppBar(title: const Text('Minha Tela')),
  body: Center(
    child: Column(
      children: [
        const Text('Olá'),
        ElevatedButton(onPressed: () {}, child: const Text('Clique')),
      ],
    ),
  ),
)
```

### O que você precisa guardar

- `Scaffold` é a estrutura principal da tela.
- `AppBar` fica no topo.
- `body` contém o conteúdo.
- `Column` organiza widgets na vertical.
- `Row` organiza widgets na horizontal.

### Mini prática

Crie uma tela com:

- um título,
- um subtítulo,
- dois botões lado a lado.

---

## 3. Layout essencial: espaçamento e alinhamento (40 min)

### Widgets que você deve praticar

- `Padding`
- `SizedBox`
- `Column`
- `Row`
- `Expanded`
- `Center`

### Exemplo

```dart
body: Padding(
  padding: const EdgeInsets.all(16),
  child: Column(
    crossAxisAlignment: CrossAxisAlignment.start,
    children: [
      const Text('Perfil do Aluno'),
      const SizedBox(height: 12),
      Row(
        children: [
          ElevatedButton(onPressed: () {}, child: const Text('Salvar')),
          const SizedBox(width: 8),
          OutlinedButton(onPressed: () {}, child: const Text('Cancelar')),
        ],
      ),
    ],
  ),
),
```

### Erros comuns

- Colocar widgets demais sem espaçamento.
- Usar `Container` vazio só para dar espaço em vez de `SizedBox`.
- Esquecer que `Column` e `Row` têm eixos diferentes.

---

## 4. Estado local com `StatefulWidget` e `setState()` (45 min)

### Ideia central

- `StatelessWidget`: a tela não muda por conta própria.
- `StatefulWidget`: a tela muda quando o estado muda.

### Exemplo com contador

```dart
class HomePage extends StatefulWidget {
  const HomePage({super.key});

  @override
  State<HomePage> createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  int contador = 0;

  void incrementar() {
    setState(() {
      contador++;
    });
  }

  void decrementar() {
    setState(() {
      if (contador > 0) {
        contador--;
      }
    });
  }
}
```

### O que você precisa guardar

- Sem `setState()`, a variável pode mudar, mas a UI não atualiza.
- `setState()` deve envolver apenas a mudança necessária.
- Nunca chame `setState()` dentro de `build()`.

---

## 5. Navegação entre duas telas (45 min)

### Conceito

O `Navigator` trabalha como uma pilha:

- `push`: entra em uma nova tela.
- `pop`: volta para a tela anterior.

### Exemplo de navegação com passagem de texto

```dart
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => DetalhesPage(item: 'Produto 1'),
  ),
);
```

### Exemplo da tela de detalhes

```dart
class DetalhesPage extends StatelessWidget {
  final String item;

  const DetalhesPage({super.key, required this.item});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Detalhes')),
      body: Center(
        child: Text(item),
      ),
    );
  }
}
```

### Erros comuns

- Esquecer o `required` no construtor.
- Passar o dado errado para a segunda tela.
- Usar `pushReplacement()` sem querer e perder a tela anterior.

---

## 6. Prática guiada da aula: contador + lista + detalhes (50 min)

Implemente este app:

### Tela Home

- título da tela,
- contador com botões `+` e `-`,
- lista com pelo menos 6 itens,
- toque em um item para abrir a tela de detalhes.

### Tela Detalhes

- mostrar o item recebido,
- botão de voltar ou AppBar com retorno.

### Estrutura sugerida

```text
lib/
- main.dart
- home_page.dart
- detalhes_page.dart
```

### Fluxo sugerido

1. Monte a `HomePage` com `Scaffold`.
2. Adicione o contador com `StatefulWidget`.
3. Crie a lista.
4. Crie a `DetalhesPage`.
5. Faça a navegação com `Navigator.push()`.
6. Teste o retorno com `Navigator.pop()`.

---

## 7. Mini checklist de autonomia (15 min)

Antes de encerrar, confirme:

- [ ] Sei explicar `Column` e `Row`.
- [ ] Usei `Padding` e `SizedBox` corretamente.
- [ ] Criei uma tela com `StatefulWidget`.
- [ ] Atualizei a UI com `setState()`.
- [ ] Naveguei da Home para a tela de detalhes.
- [ ] Voltei da tela de detalhes para a Home.
- [ ] Passei um item da lista para a segunda tela.
- [ ] Iniciei ou concluí a
      [Atividade 05](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-05).

---

## 8. Entrega da aula

Para considerar a aula concluída, o aluno deve apresentar:

- contador funcionando,
- navegação Home -> Detalhes -> Home,
- item sendo passado corretamente,
- código salvo em pasta pessoal, Drive ou GitHub,
- [Formulário Aula 03](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-03)
  preenchido.

---

## 9. Troubleshooting rápido

### Problema: a tela não atualiza

- Verifique se a mudança está dentro de `setState()`.

### Problema: erro de layout estourando

- Revise uso de `Column`, `Expanded` e listas.

### Problema: não volta para a tela anterior

- Confirme se usou `Navigator.push()` e não `pushReplacement()`.

### Problema: item não aparece na tela de detalhes

- Revise o construtor da segunda tela e o valor passado no `Navigator.push()`.

---

## 10. Guia para o professor

### Foco pedagógico

- A aula marca a transição do setup para UI funcional.
- O mais importante não é deixar a tela bonita, mas consolidar três ideias:
  layout, estado e navegação.
- Se a turma travar, priorize primeiro layout + contador, depois navegação.

### Pontos que mais geram dúvida

- diferença entre `StatelessWidget` e `StatefulWidget`,
- momento certo de usar `setState()`,
- eixos do `Row` e `Column`,
- passagem de dados para a segunda tela.

### Estratégia de condução

1. Faça uma demo curta com um contador.
2. Faça uma demo curta de navegação para uma segunda tela.
3. Depois solte a turma na atividade prática.
4. Feche a aula exigindo demonstração do fluxo completo.

---

## Estrutura do Formulário (Google Forms)

| Ordem | Pergunta                                                               | Tipo de Resposta | Observação Técnica                          |
| :---- | :--------------------------------------------------------------------- | :--------------- | :------------------------------------------ |
| 1     | Nome Completo                                                          | Resposta curta   | Identificação                               |
| 2     | Qual widget é usado para organizar elementos um abaixo do outro?       | Múltipla escolha | Resposta esperada: `Column`                 |
| 3     | Qual função reconstrói a tela após uma mudança de estado?              | Múltipla escolha | Resposta esperada: `setState()`             |
| 4     | Qual comando do Navigator é usado para voltar à tela anterior?         | Múltipla escolha | Resposta esperada: `Navigator.pop(context)` |
| 5     | Explique a principal diferença entre StatelessWidget e StatefulWidget. | Parágrafo        | Verifica compreensão                        |

---

## Dicas de ouro para o laboratório noturno

1. **Check visual rápido:** peça para os alunos te mostrarem a navegação
   funcionando antes de avançar.
2. **Separação mínima:** se der tempo, incentive a separar `HomePage` e
   `DetalhesPage` em arquivos distintos.
3. **Sem perfeccionismo:** primeiro faça funcionar, depois organize melhor.

## Materiais relacionados

- [Material 02 - Conceitos Iniciais de UI](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-02)
- [Material 16 - Arquitetura Flutter](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-16)
- [Atividade 05 - Interatividade e Navegacao (2 Telas)](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-05)
- [Formulário Aula 03](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-03)

---

**Material elaborado para o curso de PAM2 - 2026**  
Prof. Gustavo Villalta

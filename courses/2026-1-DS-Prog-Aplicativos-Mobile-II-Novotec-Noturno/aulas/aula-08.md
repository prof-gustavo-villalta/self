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

## 1. Introdução ao Mundo das APIs REST (50 min)

### Conteúdo:

- O que é uma API REST e como ela se comunica com o App.
- O formato JSON: Chave e Valor.
- Ferramentas de teste: Postman ou Insomnia (visão rápida).

### Guia para o Professor:

- **Condução Técnica:** Use uma API pública simples (ex: JSONPlaceholder) para
  mostrar o retorno no navegador. Explique que o App Flutter será o "cliente"
  que solicita esses dados.
- **Debugging:** Se a API não carregar no navegador da escola, verifique se não
  há bloqueios de firewall para domínios específicos.
- **Boas Práticas:** Antes de codificar no Flutter, sempre teste a URL da API em
  uma ferramenta externa para garantir que o endpoint está ativo.

---

## 2. Modelagem de Dados e Serialização JSON (50 min)

### Conteúdo:

- Criação da classe Model com o método `fromJson`.
- Mapeamento de campos JSON para atributos Dart.
- Lidando com tipos complexos e listas no JSON.

### Guia para o Professor:

- **Condução Técnica:** Mostre como o
  `factory Model.fromJson(Map<String, dynamic> json)` funciona. Explique que o
  `dynamic` é necessário porque o JSON pode trazer qualquer tipo de dado.
- **Debugging:** Erro clássico: `type 'int' is not a subtype of type 'String'`.
  Isso acontece quando o JSON traz um número e tentamos salvar em uma variável
  String.
- **Boas Práticas:** Use ferramentas online como o "JSON to Dart" para gerar
  modelos complexos, mas garanta que os alunos entendam a lógica manual
  primeiro.

---

## 3. O Pacote HTTP e Requisições Assíncronas (50 min)

### Conteúdo:

- Adicionando a dependência `http` no `pubspec.yaml`.
- Permissões de Internet no `AndroidManifest.xml`.
- Criando a função `fetchData()` com `async/await`.

### Guia para o Professor:

- **Condução Técnica:** Sem a permissão
  `<uses-permission android:name="android.permission.INTERNET" />`, o app
  falhará silenciosamente no Android. Mostre exatamente onde colar essa linha.
- **Debugging:** Se a requisição retornar status 404 ou 500, explique a
  diferença entre "Erro no endereço" e "Erro no servidor".
- **Boas Práticas:** Use o `Uri.parse()` para garantir que a URL seja processada
  corretamente pelo pacote HTTP.

---

## 4. Tratamento de Estados: Loading, Success e Error (50 min)

### Conteúdo:

- Gerenciamento de estado manual: `bool isLoading`, `String? errorMessage`.
- O widget `CircularProgressIndicator`.
- Tratamento de exceções com `try/catch`.

### Guia para o Professor:

- **Condução Técnica:** Implemente o fluxo: 1.
  `setState(() => isLoading = true)`, 2. Faz a chamada, 3.
  `setState(() => isLoading = false)`. Mostre como isso melhora a experiência do
  usuário.
- **Debugging:** Se o loading "girar para sempre", verifique se o `setState` de
  fechamento do loading está dentro do `finally` ou se o código travou em algum
  erro não capturado.
- **Boas Práticas:** Sempre mostre uma mensagem amigável em caso de erro, com um
  botão de "Tentar Novamente".

---

## 5. Prática Guiada: Listagem de Usuários/Postagens (50 min)

### Conteúdo:

- Desafio: Consumir um endpoint de lista e exibir em um `ListView.builder`.
- Exibir nome e e-mail de cada item vindo da API.

### Guia para o Professor:

- **Condução Técnica:** Combine o conhecimento de `ListView.builder` (Aula 04)
  com o `fetchData()`. Mostre como converter a `List<dynamic>` da resposta em
  uma `List<SeuModelo>`.
- **Debugging:** Se a lista ficar vazia, verifique se você deu o
  `notifyListeners()` ou o `setState()` após popular a lista de objetos.
- **Encerramento:** Verifique se os alunos conseguiram ver os dados reais
  aparecendo no celular.

---

## Estrutura do Formulário (Google Forms)

| Ordem | Pergunta                                                                        | Tipo de Resposta | Observação Técnica                        |
| :---- | :------------------------------------------------------------------------------ | :--------------- | :---------------------------------------- |
| 1     | Nome Completo                                                                   | Resposta curta   | Identificação                             |
| 2     | Qual o formato de dados mais utilizado para comunicação entre Apps e APIs REST? | Múltipla Escolha | JSON                                      |
| 3     | Em qual arquivo do Android devemos adicionar a permissão de INTERNET?           | Múltipla Escolha | `AndroidManifest.xml`                     |
| 4     | Para que serve o método `factory Model.fromJson(...)`?                          | Múltipla Escolha | Converter um Map (JSON) em um Objeto Dart |
| 5     | Link ou Print do seu App exibindo dados vindos de uma API real                  | Upload / Link    | Evidência de integração                   |

---

## Dicas de Ouro para o Professor (Lab Noturno)

1. **Firewall da ETEC:** Muitas APIs são bloqueadas no Wi-Fi da escola. Se isso
   acontecer, sugira que os alunos usem o roteador do próprio celular (4G/5G)
   apenas para o teste de requisição, ou usem uma API de "fallback" que você
   saiba que está liberada.
2. **Cuidado com o JSON Gigante:** Alunos se perdem em JSONs com muitas chaves.
   Comece com uma API que retorne apenas 3 ou 4 campos. O foco é o fluxo
   técnico, não a complexidade do dado.
3. **Persistência Visual:** Como requisições dependem da rede, o app pode
   parecer "morto" enquanto carrega. Reforce a obrigatoriedade do
   `CircularProgressIndicator`. No noturno, qualquer demora sem feedback visual
   faz o aluno achar que o PC travou e reiniciar a máquina.

## Materiais Relacionados

- [Material 04 - Consumo de APIs REST](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-04)
- [Atividade 08 - Consumo de API Parte 1](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-08)

---

**Material elaborado para o curso de PAM2 - 2026**  
Prof. Gustavo Villalta

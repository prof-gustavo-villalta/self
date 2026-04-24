---
layout: aula
title:
  "Aula 04 - UI com Listas Dinâmicas (ListView.builder) + Cards + Usabilidade"
course_id: mobile2
category: aulas
---

## Data e contexto

- **Data:** 08/04/2026
- **Duração:** 5 horas-aula (250 min)
- **Horário:** 18h45 às 23h10 (considerando 15 min de intervalo)
- **Laboratório:** 6

## Alinhamento com o PTD

- **Habilidades:** 1.1, 1.4
- **Bases:** Componentes visuais; navegação; organização de layout; usabilidade
  básica.

---

## 1. Do Estático ao Dinâmico: O Modelo de Dados (50 min)

### Conteúdo:

- Criação de uma classe Model (ex: `Produto`, `Tarefa`).
- Criação de uma lista de objetos em memória.
- Revisão rápida de Construtores em Dart.

### Guia para o Professor:

- **Condução Técnica:** Mostre que em um app real, os dados não estão
  "hardcoded" nos widgets. Crie uma classe `Produto` com `id`, `nome`, `preco` e
  `imagemUrl`.
- **Debugging:** Se os dados não aparecerem, verifique se a lista não está vazia
  ou se o `itemCount` do ListView está apontando para o `.length` correto da
  lista.
- **Boas Práticas:** Use `final` nos atributos da classe Model para garantir a
  imutabilidade dos dados dentro do widget.

---

## 2. ListView.builder: Eficiência e Performance (50 min)

### Conteúdo:

- Diferença entre `ListView` simples e `ListView.builder`.
- Parâmetros: `itemCount` e `itemBuilder`.
- O conceito de reciclagem de widgets (Lazy Loading).

### Guia para o Professor:

- **Condução Técnica:** Explique que o `builder` só constrói o que está visível
  na tela. Se tivermos 1000 itens, ele não pesará a memória.
- **Debugging:** Um erro comum é esquecer de retornar o widget dentro do
  `itemBuilder`. Lembre-os do `return`.
- **Boas Práticas:** Sempre defina um `itemCount`. Deixar sem pode causar erros
  de processamento infinito em alguns contextos.

---

## 3. Componentes de Lista: Card e ListTile (50 min)

### Conteúdo:

- Padronização com `Card`.
- Anatomia do `ListTile`: `leading`, `title`, `subtitle`, `trailing`.
- Adicionando imagens redondas com `CircleAvatar`.

### Guia para o Professor:

- **Condução Técnica:** O `ListTile` é o padrão ouro do Material Design para
  listas. Mostre como ele alinha automaticamente ícones e textos.
- **Debugging:** Se o `Card` ficar "colado" nas bordas da tela, envolva o
  `ListView` ou o `Card` em um `Padding`.
- **Boas Práticas:** Use `elevation` no `Card` com moderação (padrão 1 ou 2)
  para manter a interface limpa e moderna.

---

## 4. Usabilidade e Feedback Visual (50 min)

### Conteúdo:

- Feedback de toque com `InkWell` ou `onTap` do `ListTile`.
- Navegação enviando o objeto selecionado para a tela de detalhes.
- SnackBar para avisos rápidos.

### Guia para o Professor:

- **Condução Técnica:** Mostre como passar o objeto inteiro (ex: `list[index]`)
  para o construtor da tela de detalhes.
- **Debugging:** Se o toque não funcionar no `Card`, lembre que o `Card` não tem
  `onTap`. Use um `InkWell` como filho ou use o `ListTile` que já possui essa
  propriedade.
- **Boas Práticas:** Nunca deixe um botão sem ação. Se ainda não implementou,
  coloque um `print()` ou um `SnackBar` para o usuário saber que o clique
  funcionou.

---

## 5. Prática Guiada: Catálogo de Produtos (50 min)

### Conteúdo:

- Desafio: Implementar uma lista de pelo menos 10 produtos.
- Ao clicar no produto, abrir uma tela com a foto grande e a descrição completa.

### Guia para o Professor:

- **Condução Técnica:** Circule pela sala ajudando na lógica do
  `Navigator.push`. Este é o ponto onde os alunos mais se confundem com o
  `context`.
- **Debugging:** Se a imagem da URL não carregar, verifique a conexão de
  internet do celular ou se a URL é válida (HTTPS).
- **Encerramento:** Peça para os alunos mostrarem a navegação funcionando.
  Registre quem concluiu o "fluxo completo".

---

## Estrutura do Formulário (Google Forms)

| Ordem | Pergunta                                                                                     | Tipo de Resposta | Observação Técnica                 |
| :---- | :------------------------------------------------------------------------------------------- | :--------------- | :--------------------------------- |
| 1     | Nome Completo                                                                                | Resposta curta   | Identificação                      |
| 2     | Para que serve o parâmetro `itemCount` no `ListView.builder`?                                | Múltipla Escolha | Informar o tamanho da lista        |
| 3     | Qual componente do `ListTile` é geralmente usado para colocar um ícone ou imagem à esquerda? | Múltipla Escolha | `leading`                          |
| 4     | Por que usamos `ListView.builder` em vez de `ListView` para listas grandes?                  | Múltipla Escolha | Performance/Memória (Lazy Loading) |
| 5     | Link ou Print da sua lista com Cards funcionando                                             | Upload / Link    | Evidência de UI                    |

---

## Dicas de Ouro para o Professor (Lab Noturno)

1. **Problemas de Rede (Wi-Fi):** À noite, a rede da escola pode oscilar. Se as
   imagens via URL (`Image.network`) não carregarem, ensine os alunos a usarem
   imagens locais (`assets`) como fallback para não pararem o desenvolvimento.
2. **Cansaço Acumulado:** Muitos alunos vêm direto do trabalho. Faça uma pausa
   ativa de 5 min entre o Bloco 3 e 4. Peça para todos levantarem e beberem água
   para "oxigenar" a lógica.
3. **USB e Bateria:** O uso intenso do celular com depuração USB consome muita
   bateria se a porta USB do PC for fraca. Avise os alunos para conferirem se o
   celular está realmente carregando ou se precisam de uma tomada próxima.

## Materiais Relacionados

- [Material 02 - Widgets e Layout](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-02)
- [Atividade 03 - App de Listagem](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/atividade-03)

---

**Material elaborado para o curso de PAM2 - 2026**  
Prof. Gustavo Villalta

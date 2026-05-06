---
layout: atividade
title: "Atividade 08 - REST Parte 1 (GET + Lista)"
course_id: mobile2
category: atividades
deadline: "2026-05-13"
points: 10
---

## Objetivo

Construir uma tela Flutter que consome uma API REST real com `GET`, converte o
JSON em objetos Dart e exibe os dados em uma lista.

---

## Entrega mínima

Seu app deve demonstrar:

1. dependência `http` instalada;
2. permissão de internet configurada no Android;
3. classe `Usuario` com método `fromJson`;
4. service separado para buscar dados da API;
5. tela com carregamento, erro e sucesso;
6. lista de usuários vinda de `https://jsonplaceholder.typicode.com/users`.

---

## Critérios de avaliação

- **3 pts**: modelo `Usuario` correto e conversão `fromJson`;
- **3 pts**: service com requisição `GET`, `Uri.parse` e validação de status;
- **2 pts**: tela com loading, lista e botão de tentar novamente;
- **2 pts**: organização do código e evidências de funcionamento.

---

## Evidências esperadas

Envie no formulário:

- link do repositório com o código;
- print da tela carregando;
- print da lista com usuários;
- print ou descrição do teste de erro;
- resposta curta explicando para que serve o `fromJson`.

---

## Checklist antes de enviar

- [ ] O app abre sem tela vermelha.
- [ ] A URL da API abre no navegador.
- [ ] O pacote `http` está no `pubspec.yaml`.
- [ ] O Android tem permissão de internet.
- [ ] A lista mostra nome, e-mail e cidade.
- [ ] O app mostra erro quando a URL está errada.
- [ ] A URL correta foi restaurada antes do envio.

---

## Apoio rápido

- [Aula 08 - Consumo de API REST Parte 1](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/aulas/aula-08)
- [Material 04 - Consumo de APIs REST](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-04)
- [Formulário Aula 08](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-08)

---

**Prazo:** 13/05/2026

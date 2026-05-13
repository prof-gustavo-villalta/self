---
layout: atividade
title: "Atividade 09 - REST Parte 2 (Mini CRUD)"
course_id: mobile2
category: atividades
deadline: "2026-05-20"
points: 10
---

## Objetivo

Evoluir o app da Aula 08 para executar pelo menos duas acoes de escrita em uma
API REST: criar um registro com `POST` e remover um registro com `DELETE`.

---

## Entrega minima

Seu app deve demonstrar:

1. metodo `toJson` no modelo usado para enviar dados;
2. service separado com `POST` usando `Content-Type: application/json`;
3. service separado com `DELETE` usando o `id` na URL;
4. tela ou formulario simples para cadastrar um usuario;
5. confirmacao antes de excluir um item;
6. feedback visual com `SnackBar` para sucesso e erro.

> A API JSONPlaceholder aceita `POST`, `PUT` e `DELETE`, mas nao grava os dados
> de verdade. Para esta atividade, o status HTTP correto e o feedback no app sao
> as evidencias principais.

---

## Fluxo sugerido

1. Parta do projeto da Aula 08, com a lista de usuarios funcionando.
2. Confira se o modelo tem `toJson`.
3. Adicione no `ApiService` os metodos `criarUsuario` e `deletarUsuario`.
4. Crie uma tela simples de cadastro com nome e e-mail.
5. Ao salvar, chame o `POST` e mostre um `SnackBar` de sucesso.
6. Na lista, adicione um botao de excluir.
7. Antes de excluir, exiba um `showDialog` de confirmacao.
8. Ao confirmar, chame o `DELETE` e remova o item da lista local.

---

## Criterios de avaliacao

- **3 pts**: `POST` implementado corretamente com JSON e status 201;
- **2 pts**: `DELETE` implementado corretamente com `id` na URL;
- **2 pts**: UI com cadastro, confirmacao de exclusao e feedback por `SnackBar`;
- **2 pts**: tratamento de carregamento/erro durante as acoes;
- **1 pt**: organizacao do codigo em model, service e telas.

---

## Evidencias esperadas

Envie no formulario:

- link do repositorio com o codigo;
- print ou video curto do cadastro funcionando;
- print do `SnackBar` apos criar ou excluir;
- print do dialogo de confirmacao antes de excluir;
- trecho do `ApiService` com `POST` e `DELETE`;
- resposta curta explicando por que o JSONPlaceholder retorna sucesso mas nao
  persiste o registro.

---

## Checklist antes de enviar

- [ ] O app ainda lista usuarios com `GET`.
- [ ] O cadastro chama `POST` e recebe status 201.
- [ ] O `DELETE` usa o `id` correto.
- [ ] Existe confirmacao antes da exclusao.
- [ ] Existe `SnackBar` para sucesso e erro.
- [ ] O app nao trava se a internet falhar.
- [ ] O repositorio esta atualizado.

---

## Apoio rapido

- [Aula 09 - Consumo de API REST Parte 2](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/aulas/aula-09)
- [Material 04 - Consumo de APIs REST](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-04)
- [Formulário Aula 09](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-09)

---

**Prazo:** 20/05/2026

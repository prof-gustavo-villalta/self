---
layout: atividade
title: "Atividade 06 - Login + Token + Tela Protegida"
course_id: mobile2
category: atividades
deadline: "2026-04-29"
points: 10
---

## Objetivo

Implementar um fluxo completo de autenticação local em Flutter com:

- tela de login;
- feedback visual de carregamento;
- persistência de token com `shared_preferences`;
- abertura automática da Home quando já houver sessão;
- logout funcional.

---

## Entrega mínima

Seu app deve demonstrar:

1. login válido com atraso simulado;
2. mensagem de erro para credenciais inválidas;
3. token salvo no dispositivo;
4. reabertura do app caindo direto na Home;
5. logout removendo apenas a chave da sessão.

---

## Critérios de avaliação

- **4 pts**: fluxo de login com `async/await` e indicador de carregamento;
- **4 pts**: persistência e leitura do token no `main`;
- **2 pts**: organização do código, navegação correta e logout.

---

## Evidências esperadas

Envie no formulário:

- link do repositório com o código;
- link para screenshots do login, do estado de carregamento e do auto-login;
- resposta curta sobre a função do `WidgetsFlutterBinding.ensureInitialized()`.

---

## Checklist antes de enviar

- [ ] O botão `Entrar` mostra carregamento.
- [ ] O login válido abre a Home.
- [ ] O login inválido mostra erro.
- [ ] Ao fechar e abrir o app, a sessão continua.
- [ ] O botão `Sair` remove `meu_token_seguro`.

---

## Apoio rápido

- [Aula 06 - Autenticação e Persistência de Sessão](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/aulas/aula-06)
- [Material 17 - Autenticação e Sessão Local](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/materiais/material-17)
- [Formulário Aula 06](/self/courses/2026-1-DS-Prog-Aplicativos-Mobile-II-Novotec-Noturno/atividades/formulario-aula-06)

---

**Prazo:** 29/04/2026

---
layout: material
title: "Material 06 - Guia de Segurança Digital"
---

Em um mundo cada vez mais conectado, proteger suas informações pessoais e
profissionais é fundamental. Este guia apresenta boas práticas para criar senhas
seguras e utilizar recursos de proteção extras.

---

## 1. O que é uma Senha Segura?

Uma senha segura é aquela que é difícil de ser adivinhada por humanos ou
descoberta por softwares de ataque (força bruta).

### ✅ Regras de Ouro:

- **Comprimento**: Use no mínimo **12 caracteres**.
- **Complexidade**: Misture letras maiúsculas, minúsculas, números e símbolos
  (ex: `@`, `#`, `!`).
- **Aleatoriedade**: Evite sequências óbvias como `123456`, `qwerty` ou sua data
  de nascimento.
- **Exclusividade**: Nunca use a mesma senha para mais de um serviço. Se um site
  for hackeado, todos os seus outros perfis estarão em risco.

### ❌ O que NÃO usar:

- Nome de familiares ou animais de estimação.
- Placas de carros ou números de telefone.
- Palavras simples de dicionário (ex: `batata123`).

---

## 2. Técnica da "Frase-Senha" (Passphrase)

Uma das melhores formas de criar senhas longas e memoráveis é usar uma frase
curta com substituições.

**Exemplo:**

- Frase: _Eu gosto de programar no Flutter_
- Senha gerada: `EuG0st0#Pr0gramar!FL`

---

## 3. Autenticação em Duas Etapas (2FA/MFA)

A autenticação em duas etapas é uma camada extra de segurança. Mesmo que alguém
descubra sua senha, não conseguirá acessar sua conta sem o segundo fator.

### Tipos comuns de 2FA:

1. **Apps Autenticadores (Recomendado)**: Google Authenticator, Microsoft
   Authenticator ou Authy. Eles geram códigos temporários que mudam a cada 30
   segundos.
2. **SMS**: Recebimento de código por mensagem (menos seguro que apps, mas
   melhor que nada).
3. **Chaves Físicas**: Dispositivos USB como o YubiKey.

**Onde ativar primeiro?**

- E-mail principal (Gmail/Outlook).
- Redes Sociais (Instagram, WhatsApp, LinkedIn).
- Bancos e sites de compras.

---

## 4. Proteção contra Fraudes (Phishing)

O **Phishing** é uma técnica onde criminosos fingem ser empresas confiáveis para
roubar seus dados.

### Como identificar um ataque:

- **Urgência**: Mensagens que dizem "Sua conta será bloqueada AGORA" ou "Você
  ganhou um prêmio, clique aqui".
- **Remetente Estranho**: Verifique o endereço de e-mail. Se diz ser do Banco X,
  mas o e-mail termina em `@gmail.com` ou `@servidor-estranho.com`, desconfie.
- **Erros de Português**: Empresas grandes costumam revisar muito bem seus
  textos.
- **Links Suspeitos**: Passe o mouse sobre o link (sem clicar) para ver o
  endereço real no rodapé do navegador.

---

## 5. Como saber se minha senha vazou?

Muitas vezes, grandes empresas sofrem ataques e os e-mails e senhas dos usuários
são expostos na internet.

### 🕵️ Have I Been Pwned (HIBP)

O site [Have I Been Pwned](https://haveibeenpwned.com/) é o serviço mais
confiável do mundo para verificar se seu e-mail ou telefone já apareceu em algum
vazamento de dados conhecido.

- **O que fazer se o resultado for vermelho (Pwned)?**
  1. Não entre em pânico.
  2. Mude a senha daquele serviço imediatamente.
  3. Ative a autenticação em duas etapas (2FA).
  4. Mude a senha de outros sites onde você usava a mesma combinação (o que
     reforça a regra de nunca repetir senhas!).

---

## 6. Gerenciadores de Senhas

Como é impossível decorar dezenas de senhas complexas, recomendamos o uso de
gerenciadores. Eles guardam todas as suas senhas em um "cofre" criptografado e
você só precisa decorar **uma** senha mestra (que deve ser muito forte).

**Sugestões Gratuitas:**

- **Bitwarden** (Código aberto e muito seguro).
- **KeePassXC** (Para uso offline).
- **Google Password Manager** (Integrado ao Chrome/Android).

---

## 📝 Atividade Prática: Diagnóstico de Segurança

1. **Verificação de Vazamentos**: Acesse o site
   [haveibeenpwned.com](https://haveibeenpwned.com/) e digite seu e-mail
   principal (pessoal ou institucional).
   - Se o resultado for **verde**: Ótimo! Seus dados não apareceram em
     vazamentos conhecidos.
   - Se o resultado for **vermelho**: Veja a lista de sites abaixo do campo de
     busca e identifique quais serviços foram comprometidos.
2. **Ação Corretiva**: Se você teve contas "pwned", verifique se ainda usa
   aquela senha em outros sites e realize a troca agora.
3. **WhatsApp e Redes Sociais**: Ative a autenticação em duas etapas no seu
   WhatsApp (Configurações > Conta > Confirmação em duas etapas) e no seu
   Instagram.
4. **Gerenciador**: Escolha um gerenciador de senhas e comece a cadastrar suas
   contas principais para evitar o uso de senhas repetidas.

---

**Material elaborado para o curso de PTIC - 2026**  
Prof. Gustavo Villalta

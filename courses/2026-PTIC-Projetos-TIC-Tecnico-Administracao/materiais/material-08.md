---
layout: material
title: "Material 08 - Guia de Produtividade com Google Workspace"
---

# 📊 Guia de Produtividade com Google Workspace

Este guia ensina o uso completo das ferramentas de produtividade do Google
Workspace (Docs, Sheets, Slides) aplicadas ao contexto administrativo e
acadêmico.

---

## 📄 Google Docs - Documentos de Texto

### Acesso

- Acesse: [docs.google.com](https://docs.google.com)
- Ou: Drive → Novo → Documento Google

### Interface Principal

```
┌─────────────────────────────────────────────────────────────┐
│  Arquivo  Editar  Ver  Inserir  Formatar  Ferramentas  Ajuda │
├─────────────────────────────────────────────────────────────┤
│  Nome do Documento                    Compartilhar  👤      │
├─────────────────────────────────────────────────────────────┤
│  ↩️ ↪️ 🖨️ ⬆️ 💾    Título Normal  Arial  11  🅱️ 🅸 Ⓤ        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Área de edição do documento                                │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Formatação Essencial

#### Estilos de Parágrafo

| Estilo    | Uso                  | Atalho         |
| --------- | -------------------- | -------------- |
| Título    | Nome do documento    | Ctrl + Alt + 1 |
| Subtítulo | Descrição breve      | Ctrl + Alt + 2 |
| Título 1  | Capítulos principais | Ctrl + Alt + 1 |
| Título 2  | Seções               | Ctrl + Alt + 2 |
| Título 3  | Subseções            | Ctrl + Alt + 3 |
| Normal    | Texto comum          | Ctrl + Alt + 0 |

> 💡 **Dica:** Use estilos em vez de formatar manualmente (negrito, tamanho).
> Isso cria sumário automaticamente!

#### Formatação de Texto

- **Negrito:** `Ctrl + B`
- _Itálico:_ `Ctrl + I`
- <u>Sublinhado:</u> `Ctrl + U`
- ~~Tachado:~~ `Alt + Shift + 5`
- `Código:` `Ctrl + ,`

#### Listas

- **Lista com marcadores:** `Ctrl + Shift + 8`
- **Lista numerada:** `Ctrl + Shift + 7`
- **Lista de verificação:** `Ctrl + Shift + 9`

---

### Recursos Avançados

#### Inserir Sumário

1. Clique em **Inserir** → **Sumário**
2. Escolha: Com números de página ou Links azuis
3. O sumário atualiza automaticamente!

#### Cabeçalho e Rodapé

1. **Inserir** → **Cabeçalho e rodapé**
2. Adicione:
   - Número de página
   - Nome do documento
   - Data
   - Logo da empresa

#### Comentários

- Selecione o texto
- `Ctrl + Alt + M` ou clique em 💬
- Útil para revisões em equipe

#### Modo de Sugestões (Revisão)

1. Clique em **Sugestão** (canto superior direito)
2. Todas as alterações ficam em verde
3. O dono do documento pode aceitar ou rejeitar

---

### Compartilhamento e Colaboração

| Permissão        | O que a pessoa pode fazer   |
| ---------------- | --------------------------- |
| **Visualizador** | Só ler, não pode editar     |
| **Comentarista** | Ler e adicionar comentários |
| **Editor**       | Ler, editar, compartilhar   |

**Como compartilhar:**

1. Clique em **Compartilhar** (canto superior direito)
2. Digite os e-mails
3. Escolha a permissão
4. Clique em **Enviar**

**Link público:**

1. Em Compartilhar, clique em **Alterar** (ao lado de "Restrito")
2. Selecione "Qualquer pessoa com o link"
3. Escolha a permissão desejada
4. Copie o link

---

## 📈 Google Sheets - Planilhas

### Acesso

- [sheets.google.com](https://sheets.google.com)
- Ou: Drive → Novo → Planilha

### Conceitos Básicos

```
    A      B      C      D
1  Nome   Idade  Cargo  Salário
2  Ana    25     Dev    R$ 5.000
3  Bruno  30     Design R$ 4.500
```

| Termo         | Significado                      |
| ------------- | -------------------------------- |
| **Célula**    | Caixinha individual (ex: A1, B2) |
| **Linha**     | Horizontal (números 1, 2, 3...)  |
| **Coluna**    | Vertical (letras A, B, C...)     |
| **Intervalo** | Grupo de células (ex: A1:D10)    |
| **Fórmula**   | Começa com = (igual)             |

---

### Fórmulas Essenciais

#### Fórmulas Básicas

```
=SOMA(A1:A10)           → Soma valores de A1 até A10
=MÉDIA(B1:B10)          → Calcula a média
=MÁXIMO(C1:C10)         → Maior valor
=MÍNIMO(D1:D10)         → Menor valor
=CONT.VALORES(E1:E10)   → Conta células preenchidas
```

#### Fórmulas Lógicas

```
=SE(A1>10; "Aprovado"; "Reprovado")
→ Se A1 for maior que 10, mostra "Aprovado", senão "Reprovado"

=E(A1>0; A1<100)        → Verifica se A1 está entre 0 e 100
=OU(A1="Sim"; A1="S")   → Verifica se A1 é "Sim" OU "S"
```

#### Fórmulas de Texto

```
=CONCATENAR(A1; " "; B1)  → Junta A1, espaço e B1
=ESQUERDA(A1; 3)          → Pega 3 primeiros caracteres
=DIREITA(A1; 4)           → Pega 4 últimos caracteres
=MAIÚSCULA(A1)            → Converte para maiúsculas
```

#### Fórmulas de Data

```
=HOJE()                   → Data atual
=AGORA()                  → Data e hora atual
=ANO(A1)                  → Extrai o ano da data em A1
=MÊS(A1)                  → Extrai o mês
=DIA(A1)                  → Extrai o dia
=DIA.DA.SEMANA(A1)        → Dia da semana (1=Domingo)
```

#### PROCV (Busca Vertical)

```
=PROCV("Ana"; A1:D10; 3; FALSO)
→ Procura "Ana" na primeira coluna de A1:D10
→ Retorna o valor da 3ª coluna
→ FALSO = procura exata
```

---

### Formatação Condicional

Destaque células automaticamente baseado em regras:

1. Selecione as células
2. **Formatar** → **Formatação condicional**
3. Escolha a regra:
   - **Escala de cores:** Verde (bom) → Vermelho (ruim)
   - **Escala de valores:** Maior que, menor que, igual a
   - **Texto contém:** Destaca células com texto específico

**Exemplo prático:**

- Valores > 1000 → Fundo verde 🟢
- Valores < 0 → Fundo vermelho 🔴
- Texto "Atrasado" → Fundo amarelo 🟡

---

### Gráficos

1. Selecione os dados
2. **Inserir** → **Gráfico**
3. Escolha o tipo:

| Tipo de Gráfico  | Quando Usar                          |
| ---------------- | ------------------------------------ |
| **Coluna/Barra** | Comparar valores                     |
| **Linha**        | Mostrar tendências ao longo do tempo |
| **Pizza**        | Mostrar proporções/partes de um todo |
| **Dispersão**    | Relação entre duas variáveis         |

---

### Dicas Avançadas

#### Congelar Linhas/Colunas

- **Visualizar** → **Congelar**
- Mantém cabeçalhos visíveis ao rolar

#### Proteger Planilha

- **Ferramentas** → **Proteger planilha**
- Impede edições acidentais

#### Validação de Dados

1. Selecione a célula
2. **Dados** → **Validação de dados**
3. Defina regras (ex: só números, só datas, lista suspensa)

#### Filtros

- Selecione os dados
- **Dados** → **Filtro**
- Aparecem setas no cabeçalho para filtrar

---

## 🎨 Google Slides - Apresentações

### Acesso

- [slides.google.com](https://slides.google.com)
- Ou: Drive → Novo → Apresentação

### Princípios de Design

#### Regra 6x6

- **Máximo 6 linhas** por slide
- **Máximo 6 palavras** por linha

#### Contraste

- Fundo escuro → Texto claro
- Fundo claro → Texto escuro
- Evite fundos com imagens poluídas

#### Cores

- Use no máximo **3 cores principais**
- Use a paleta da sua marca/empresa
- Cores sugeridas:
  - **Azul:** Confiança, profissionalismo
  - **Verde:** Crescimento, sucesso
  - **Vermelho:** Atenção, urgência
  - **Amarelo:** Otimismo, criatividade

---

### Elementos Visuais

#### Inserir Imagens

1. **Inserir** → **Imagem**
2. Opções:
   - Fazer upload (do computador)
   - Pesquisar na web
   - Google Drive
   - Câmera
   - Por URL

> ⚠️ **Atenção:** Use imagens de alta qualidade (evite pixeladas)

#### Formas e Diagramas

- **Inserir** → **Forma**
- Use setas para mostrar fluxo
- Use retângulos arredondados para caixas de texto
- Use círculos para destacar

#### SmartArt (Diagramas)

1. **Inserir** → **Diagrama**
2. Escolha o tipo:
   - **Hierarquia:** Organogramas
   - **Relacionamento:** Venn, setas
   - **Ciclo:** Processos circulares
   - **Linha do tempo:** Cronologia

---

### Animações e Transições

#### Transições entre Slides

1. Clique no slide
2. **Transição** (menu lateral)
3. Escolha o efeito:
   - **Dissolver:** Suave, profissional
   - **Deslizar:** Direcional
   - **Zoom:** Impactante

> 💡 **Dica:** Use a mesma transição para todos os slides (consistência)

#### Animações de Elementos

1. Selecione o elemento
2. **Animação** (menu lateral)
3. Escolha:
   - **Ao clicar:** Aparece quando você clica
   - **Com anterior:** Aparece junto com o elemento anterior
   - **Depois de anterior:** Aparece automaticamente depois

> ⚠️ **Cuidado:** Poucas animações! Muitas distraem.

---

### Modo Apresentação

#### Atalhos durante a apresentação

| Tecla           | Ação               |
| --------------- | ------------------ |
| `→` ou `Espaço` | Próximo slide      |
| `←`             | Slide anterior     |
| `Esc`           | Sair               |
| `B`             | Tela preta (pausa) |
| `W`             | Tela branca        |
| `L`             | Laser pointer      |

#### Apresentar com legenda

- **Apresentar** → **Legendas ao vivo**
- O Google transcreve automaticamente o que você fala!

---

## 🔄 Integração entre Ferramentas

### Do Sheets para o Docs

1. No Sheets, copie a tabela (`Ctrl + C`)
2. No Docs, cole (`Ctrl + V`)
3. Escolha:
   - **Colar:** Tabela editável vinculada
   - **Colar sem formatação:** Somente texto
   - **Colar como imagem:** Não editável

### Do Slides para o Docs

- Copie o slide como imagem
- Cole no Docs

### Importar do Word/Excel/PowerPoint

1. Drive → Novo → Upload de arquivo
2. O Google converte automaticamente!
3. Ou: Abra o arquivo e clique em "Abrir com" → Google Docs/Sheets/Slides

---

## 📱 Atalhos de Teclado Essenciais

### Todos os Aplicativos

| Atalho     | Ação                                           |
| ---------- | ---------------------------------------------- |
| `Ctrl + Z` | Desfazer                                       |
| `Ctrl + Y` | Refazer                                        |
| `Ctrl + F` | Procurar                                       |
| `Ctrl + P` | Imprimir                                       |
| `Ctrl + S` | Salvar (salva automaticamente, mas força save) |

### Google Docs Específico

| Atalho           | Ação                 |
| ---------------- | -------------------- |
| `Ctrl + B`       | Negrito              |
| `Ctrl + I`       | Itálico              |
| `Ctrl + U`       | Sublinhado           |
| `Ctrl + K`       | Inserir link         |
| `Ctrl + Alt + C` | Contagem de palavras |

### Google Sheets Específico

| Atalho             | Ação                         |
| ------------------ | ---------------------------- |
| `Ctrl + ;`         | Inserir data atual           |
| `Ctrl + Shift + ;` | Inserir hora atual           |
| `Ctrl + D`         | Preencher para baixo         |
| `Ctrl + R`         | Preencher para direita       |
| `F4`               | Travar referência (absoluta) |

---

## 🎯 Exercício Prático

### Cenário: Organização de Evento

Você está organizando a **Festinha Junina da ETEC 2026**.

**Tarefa 1 - Planilha (Sheets):**

1. Crie uma planilha chamada "Festa-Junina-2026-Orçamento"
2. Colunas: Item, Quantidade, Valor Unitário, Valor Total
3. Itens: Decoração, Comida, Bebida, Som, Brinquedos
4. Use fórmulas para calcular o Total
5. Crie um gráfico de pizza mostrando a distribuição dos gastos

**Tarefa 2 - Documento (Docs):**

1. Crie um documento "Festa-Junina-2026-Relatório"
2. Use estilos de título adequados
3. Insira uma introdução, desenvolvimento e conclusão
4. Cole a tabela e o gráfico da planilha
5. Adicione cabeçalho com nome da escola e rodapé com número de página

**Tarefa 3 - Apresentação (Slides):**

1. Crie 5 slides apresentando o evento
2. Slide 1: Título
3. Slide 2: Objetivo do evento
4. Slide 3: Programação
5. Slide 4: Orçamento (com gráfico)
6. Slide 5: Agradecimentos

---

## 📚 Recursos Complementares

### Templates Oficiais

- [Google Docs Templates](https://docs.google.com/document/u/0/?ftv=1&tgif=c)
- [Google Sheets Templates](https://sheets.google.com/template/gallery)
- [Google Slides Templates](https://slides.google.com/theme)

### Cursos Gratuitos

- [Google Workspace Learning Center](https://support.google.com/a/users/answer/9282669)
- [Applied Digital Skills (Google)](https://applieddigitalskills.withgoogle.com/)

---

**Material elaborado para PTIC - 2026**  
Prof. Gustavo Villalta

---
layout: material
title: "Material 11 - Excel e Google Sheets: Fórmulas e Funções"
---

# 📊 Excel e Google Sheets: Fórmulas, Funções e Gráficos

Guia completo para dominar planilhas eletrônicas, com foco em fórmulas, funções
avançadas, análise de dados e criação de gráficos profissionais.

---

## Conceitos Fundamentais

### Estrutura da Planilha

```
    A      B        C         D
1  Nome   Nota 1   Nota 2    Média
2  Ana    8,5      9,0       =MÉDIA(B2:C2)
3  Bruno  7,0      8,5       =MÉDIA(B3:C3)
```

| Elemento      | Descrição                 | Exemplo        |
| ------------- | ------------------------- | -------------- |
| **Célula**    | Interseção linha x coluna | A1, B2, C10    |
| **Intervalo** | Grupo de células          | A1:C10, B2:B10 |
| **Fórmula**   | Começa com =              | =A1+B1         |
| **Função**    | Comando predefinido       | =SOMA(A1:A10)  |

---

## Fórmulas Básicas

### Operadores Matemáticos

| Operador | Função        | Exemplo    | Resultado |
| -------- | ------------- | ---------- | --------- |
| `+`      | Adição        | `=5+3`     | 8         |
| `-`      | Subtração     | `=10-4`    | 6         |
| `*`      | Multiplicação | `=6*7`     | 42        |
| `/`      | Divisão       | `=20/4`    | 5         |
| `^`      | Potência      | `=2^3`     | 8         |
| `%`      | Porcentagem   | `=100*10%` | 10        |

### Referências de Células

```
Referência        | Exemplo       | Comportamento ao copiar
------------------|---------------|-------------------------
Relativa          | A1            | Muda (A1 → A2 → A3)
Absoluta          | $A$1          | Fixa (sempre A1)
Mista Linha       | A$1           | Coluna muda, linha fixa
Mista Coluna      | $A1           | Coluna fixa, linha muda
```

**Dica**: Pressione F4 (Excel) ou F4 (Sheets) para alternar entre tipos de
referência.

---

## Funções Essenciais

### 1. Funções de Matemática e Estatística

```excel
=SOMA(A1:A10)           → Soma valores do intervalo
=MÉDIA(B2:B20)          → Calcula a média aritmética
=MED(C1:C100)           → Encontra a mediana
=MÁXIMO(D1:D50)         → Maior valor
=MÍNIMO(E1:E50)         → Menor valor
=CONT.VALORES(F1:F30)   → Conta células com dados
=CONT.NÚM(G1:G30)       → Conta apenas números
=MULT(A1:A5)            → Multiplica todos os valores
=SOMAQUAD(H1:H10)       → Soma dos quadrados
```

### 2. Funções de Texto

```excel
=CONCATENAR(A1; " "; B1)     → Une textos (João Silva)
=TEXTOUNIR(A1:A5; ", ")      → Une intervalo com separador
=ESQUERDA("ETEC", 2)         → Extrai caracteres da esquerda (ET)
=DIREITA("Americana", 4)     → Extrai da direita (cana)
=EXT.TEXTO("Polivalente", 5, 4) → Extrai do meio (lent)
=MAIÚSCULA("etec")           → ETEC
=MINÚSCULA("ETEC")           → etec
=PRI.MAIÚSCULA("americana")  → Americana
=ARRUMAR("  texto  ")        → Remove espaços extras
=SUBSTITUIR("2024"; "24"; "25") → Substitui texto
```

### 3. Funções de Data e Hora

```excel
=HOJE()                      → Data atual (dd/mm/aaaa)
=AGORA()                     → Data e hora atual
=DIA(A1)                     → Extrai o dia
=MÊS(A1)                     → Extrai o mês
=ANO(A1)                     → Extrai o ano
=DIASEM(A1)                  → Dia da semana (1=Domingo)
=NOMEDIASEM(A1)              → Nome do dia (segunda-feira)
=FIMMÊS(A1; 0)               → Último dia do mês
=DATADIF(A1; B1; "D")        → Diferença em dias
=DATADIF(A1; B1; "M")        → Diferença em meses
=DATADIF(A1; B1; "Y")        → Diferença em anos
=DIATRABALHO(A1; 10)         → Data após 10 dias úteis
```

### 4. Funções de Pesquisa e Referência

```excel
=PROCV("João"; A1:D100; 3; FALSO)    → Busca vertical
=PROCH("Jan"; A1:M5; 2; FALSO)       → Busca horizontal
=ÍNDICE(A1:D100; 5; 3)               → Valor na linha 5, coluna 3
=CORRESP("João"; A1:A100; 0)         → Posição do valor
=INDIRETO("A"&B1)                    → Referência dinâmica
=DESLOC(A1; 2; 3)                    → Desloca 2 linhas, 3 colunas
```

**PROCV Explicado:**

```
=PROCV(o_que_procurar; onde_procurar; coluna_retorno; correspondência)

=PROCV("Notebook"; A2:D50; 3; FALSO)
         ↑                ↑    ↑     ↑
    Procura "Notebook"   |    |     Correspondência exata
       na coluna A       |    Retorna coluna 3 (preço)
              da tabela A2:D50
```

### 5. Funções Lógicas (SE, E, OU)

```excel
=SE(A1>=7; "Aprovado"; "Reprovado")
→ Se nota >= 7, retorna "Aprovado", senão "Reprovado"

=SE(E(A1>=7; B1>=7); "Aprovado"; "Reprovado")
→ Aprovado apenas se A1 E B1 forem >= 7

=SE(OU(A1>=7; B1>=7); "Aprovado"; "Reprovado")
→ Aprovado se A1 OU B1 for >= 7

=SE(E(A1>=7; A1<9); "Bom"; SE(A1>=9; "Excelente"; "Regular"))
→ Encadeamento de SE (nested IF)

=SEERRO(PROCV(...); "Não encontrado")
→ Trata erro se valor não existir
```

### 6. Funções Financeiras

```excel
=PGTO(0,02; 24; 10000)           → Prestação de empréstimo
=VF(0,01; 12; -100; -1000)       → Valor futuro
=VP(0,01; 12; -100)              → Valor presente
=NPER(0,01; -100; 1000)          → Número de períodos
=TAXA(12; -100; 1000)            → Taxa de juros
```

---

## Exemplos Práticos

### Exemplo 1: Controle de Estoque

| Produto | Qtd Inicial | Entradas | Saídas | Qtd Atual   | Status                      |
| ------- | ----------- | -------- | ------ | ----------- | --------------------------- |
| Caneta  | 100         | 50       | 30     | `=B2+C2-D2` | `=SE(E2<20;"COMPRAR";"OK")` |

**Fórmulas:**

- Qtd Atual: `=B2+C2-D2`
- Status: `=SE(E2<20;"COMPRAR";"OK")` (com formatação condicional)

### Exemplo 2: Folha de Pagamento

| Funcionário | Salário Bruto | INSS (11%) | IR                              | Salário Líquido |
| ----------- | ------------- | ---------- | ------------------------------- | --------------- |
| João        | 5000          | `=B2*0,11` | `=SE(B2>4000;B2*0,15;B2*0,075)` | `=B2-C2-D2`     |

### Exemplo 3: Controle de Vendas

```excel
=SOMASE(C2:C100; "Vendedor A"; D2:D100)
→ Soma vendas apenas do Vendedor A

=CONT.SE(B2:B100; ">1000")
→ Conta quantas vendas foram acima de 1000

=MÉDIASE(C2:C100; "Eletrônicos"; D2:D100)
→ Média de vendas da categoria Eletrônicos
```

---

## Gráficos

### Tipos de Gráficos e Quando Usar

| Tipo          | Uso Ideal                  | Exemplo                 |
| ------------- | -------------------------- | ----------------------- |
| **Colunas**   | Comparar valores           | Vendas por mês          |
| **Barras**    | Comparar categorias        | Produtos mais vendidos  |
| **Linhas**    | Mostrar tendências         | Evolução de vendas      |
| **Pizza**     | Proporções/partes          | Participação de mercado |
| **Dispersão** | Correlação entre variáveis | Idade vs. Gasto         |
| **Área**      | Evolução acumulada         | Crescimento acumulado   |

### Como Criar um Gráfico (Google Sheets)

1. **Selecione os dados** (inclua cabeçalhos)
2. Clique em **Inserir → Gráfico**
3. O Google Sheets sugere o tipo automaticamente
4. No painel lateral, customize:
   - Tipo de gráfico
   - Títulos dos eixos
   - Cores
   - Legenda

### Como Criar um Gráfico (Excel)

1. **Selecione os dados**
2. Vá para a aba **Inserir**
3. Escolha o tipo no grupo **Gráficos**
4. Use o botão **Elementos do Gráfico** (+) para adicionar:
   - Título
   - Rótulos de dados
   - Tabela de dados
   - Linha de tendência

### Gráficos Combinados

Combine colunas e linhas no mesmo gráfico:

```
Colunas: Vendas
Linha: Meta
```

**No Excel:**

1. Crie o gráfico de colunas
2. Clique na série que será linha
3. Altere tipo para "Linha com Marcadores"
4. Marque "Eixo Secundário" se necessário

---

## Formatação Condicional

Destaque células automaticamente baseado em regras:

### Regras Comuns

```
Regra: Valor > 1000
Formato: Fundo verde

Regra: Valor < 0
Formato: Fundo vermelho, texto branco

Regra: Texto contém "Atrasado"
Formato: Fundo amarelo

Regra: Data é anterior a HOJE()
Formato: Texto cinza tachado
```

### Escala de Cores (Heat Map)

Excel: **Página Inicial → Formatação Condicional → Escala de Cores**

Sheets: **Formatar → Formatação condicional → Escala de cores**

---

## Validação de Dados

Evite erros de digitação restringindo entradas:

### No Excel:

**Dados → Validação de Dados**

### No Google Sheets:

**Dados → Validação de dados**

### Exemplos de Validação

1. **Lista suspensa:**
   - Permitir: Lista
   - Fonte: `Sim,Não,Talvez`

2. **Números entre 0 e 100:**
   - Permitir: Número decimal
   - Entre: 0 e 100

3. **Datas futuras:**
   - Permitir: Data
   - Maior que: `=HOJE()`

4. **Texto específico:**
   - Permitir: Texto
   - Comprimento: igual a 11 (CPF)

---

## Tabelas Dinâmicas

Resuma grandes volumes de dados rapidamente.

### Criar Tabela Dinâmica (Excel)

1. Selecione os dados
2. **Inserir → Tabela Dinâmica**
3. Arraste campos para:
   - **Linhas**: Categorias (ex: Produto)
   - **Colunas**: Períodos (ex: Mês)
   - **Valores**: Dados (ex: Soma de Vendas)
   - **Filtros**: Filtros gerais

### Criar Tabela Dinâmica (Google Sheets)

1. Selecione os dados
2. **Inserir → Tabela dinâmica**
3. Configure no painel lateral

---

## Atalhos Essenciais

| Atalho                 | Excel                 | Google Sheets    |
| ---------------------- | --------------------- | ---------------- |
| Inserir linha          | Ctrl + Shift + +      | Ctrl + Alt + =   |
| Excluir linha          | Ctrl + -              | Ctrl + Alt + -   |
| Preencher para baixo   | Ctrl + D              | Ctrl + D         |
| Preencher para direita | Ctrl + R              | Ctrl + R         |
| Selecionar tudo        | Ctrl + Shift + Espaço | Ctrl + A         |
| Inserir data           | Ctrl + ;              | Ctrl + ;         |
| Inserir hora           | Ctrl + Shift + ;      | Ctrl + Shift + ; |
| Editar célula          | F2                    | F2               |
| Ir para                | Ctrl + G              | Ctrl + Alt + G   |
| Localizar/Substituir   | Ctrl + H              | Ctrl + H         |

---

## Exercício Prático Completo

Crie uma planilha de **Controle de Vendas Mensal** com:

### Dados:

| Mês | Vendedor | Produto  | Categoria   | Quantidade | Preço Unit | Total   |
| --- | -------- | -------- | ----------- | ---------- | ---------- | ------- |
| Jan | Ana      | Notebook | Informática | 5          | 3500       | =E2\*F2 |

### Requisitos:

1. **Fórmulas Básicas:**
   - Calcule Total (Quantidade × Preço)
   - Calcule Comissão (10% do Total)

2. **Funções de Resumo:**
   - Total de vendas do mês (=SOMA)
   - Média de vendas por vendedor (=MÉDIA)
   - Produto mais vendido (=MÁXIMO)

3. **PROCV:**
   - Crie uma tabela auxiliar com Código → Nome do Produto
   - Use PROCV para buscar nome pelo código

4. **SE:**
   - Classifique: "Bom" se Total > 10000, "Regular" se > 5000, "Baixo" senão

5. **Gráfico:**
   - Crie gráfico de colunas comparando vendedores
   - Adicione linha de meta (valor fixo)

6. **Formatação Condicional:**
   - Destaque vendas acima de 10000 em verde
   - Destaque vendas abaixo de 3000 em vermelho

---

## Dicas de Produtividade

### Trava de Referência (F4)

Pressione F4 ao criar fórmulas para travar referências:

```
A1 → $A$1 → A$1 → $A1 → A1 (ciclo)
```

### Copiar Fórmulas

- Arraste a alça de preenchimento (quadradinho no canto)
- Duplo clique na alça para preencher automaticamente

### Nomear Intervalos

Dê nomes significativos a células/intervalos:

1. Selecione A1:A10
2. Caixa de nome (esquerda da fórmula) → digite "Precos"
3. Use `=SOMA(Precos)` nas fórmulas

### Proteger Planilha

**Excel:** Revisar → Proteger Planilha **Sheets:** Ferramentas → Proteger
planilha

---

## Referências

- **Google Sheets Help:**
  [support.google.com/docs](https://support.google.com/docs)
- **Excel Support:**
  [support.microsoft.com/excel](https://support.microsoft.com/excel)
- **Excel Easy:** [exceleasy.com](https://www.exceleasy.com)
- **Planilhas Google:**
  [google.com/sheets/about](https://www.google.com/sheets/about/)

---

**Material elaborado para PTIC - 2026**  
Prof. Gustavo Villalta

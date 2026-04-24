---
layout: material
title: "Material 03 - Guia de Nomenclatura"
---

## Regras Básicas

### ✅ Fazer:

- ✓ Use nomes descritivos e claros
- ✓ Inclua data no formato **AAAA-MM-DD**
- ✓ Use **hífens** (-) ou **underscores** (\_) - não use espaços
- ✓ Mantenha consistência em todo o projeto
- ✓ Use letras maiúsculas para prefixos identificadores

### ❌ Evitar:

- ✗ Espaços em branco
- ✗ Caracteres especiais: ! @ # $ % ¨ & \* ( ) + = ? / \ | < >
- ✗ Nomes genéricos: "documento", "arquivo", "novo", "final"
- ✗ Letras maiúsculas e minúsculas misturadas no meio
- ✗ Abreviações sem padrão

---

## Padrões por Tipo

### 1. Documentos Administrativos

```
TIPO-AAAA-MM-DD-DESCRICAO.ext

Exemplos:
REL-2026-03-25-Relatorio-Vendas-Mensal.docx
ATA-2026-03-20-Reuniao-Diretoria.pdf
CON-2026-03-15-Contrato-Fornecedor.docx
MEM-2026-03-10-Memorando-Circular.docx
OFI-2026-03-05-Oficio-Resposta-Solicitacao.docx
```

**Prefixos comuns:** | Prefixo | Significado | |---------|-------------| | REL |
Relatório | | ATA | Ata de reunião | | CON | Contrato | | MEM | Memorando | |
OFI | Ofício | | REQ | Requisição | | SOL | Solicitação |

### 2. Planilhas e Dados

```
TIPO-AAAA-MM-DD-DESCRICAO.xlsx

Exemplos:
PLAN-2026-03-25-Controle-Estoque.xlsx
ORC-2026-03-20-Orcamento-Anual.xlsx
DADOS-2026-03-15-Clientes-Cadastrados.xlsx
```

### 3. Projetos

```
PROJETO-NOME-AA/versao-descricao.ext

Exemplos:
PROJETO-Marketing-26/v1.0-proposta-inicial.pptx
PROJETO-Marketing-26/v1.1-proposta-revisada.pptx
PROJETO-Marketing-26/v2.0-proposta-final.pptx
```

### 4. Arquivos Pessoais

```
AAAA-MM-DD_DESCRICAO.ext

Exemplos:
2026-03-25_Comprovante-Pagamento-Energia.pdf
2026-03-20_Foto-Aniversario-Maria.jpg
2026-03-15_Recibo-Aluguel-Marco.pdf
```

### 5. Atividades Escolares

```
DISCIPLINA-AA-TURMA-AULA-NN-DESCRICAO.ext

Exemplos:
PTIC-26-TA-AULA-01-Exercicio-Organizacao.docx
PTIC-26-TA-PROJ-01-Portifolio-Digital.pptx
ADM-26-TB-TRAB-02-Analise-SWOT.xlsx
```

---

## Estrutura de Pastas Sugerida

### Para Projetos:

```
📁 PROJETO-Nome-Projeto-AA/
├── 📁 00_ADM/
│   ├── 📁 Contratos/
│   └── 📁 Correspondencias/
├── 📁 01_PLANEJAMENTO/
│   ├── 📁 Cronograma/
│   └── 📁 Reunioes/
├── 📁 02_EXECUCAO/
│   ├── 📁 Entregas/
│   └── 📁 Revisoes/
├── 📁 03_DOCUMENTACAO/
│   ├── 📁 Manuais/
│   └── 📁 Relatorios/
├── 📁 04_MIDIA/
│   ├── 📁 Imagens/
│   └── 📁 Videos/
└── 📁 99_ARQUIVADOS/
```

### Para Documentos Pessoais:

```
📁 Documentos/
├── 📁 Pessoal/
│   ├── 📁 RG-CPF/
│   ├── 📁 Certidoes/
│   ├── 📁 Diplomas/
│   └── 📁 Contratos/
├── 📁 Financeiro/
│   ├── 📁 2026/
│   │   ├── 📁 Impostos/
│   │   ├── 📁 Contas/
│   │   └── 📁 Comprovantes/
│   └── 📁 2025/
├── 📁 Saude/
│   ├── 📁 Exames/
│   └── 📁 Receitas/
└── 📁 Trabalho/
    ├── 📁 Curriculo/
    └── 📁 Certificados/
```

---

## Exemplos Completos

### ❌ Antes (Ruim):

```
documento final.docx
Nova pasta (2)
trabalho.docx
imagem.jpg
proposta.pptx
relatorio_final_CORRIGIDO.docx
```

### ✅ Depois (Bom):

```
PROJETO-Marketing-26/
├── 📁 01_PLANEJAMENTO/
│   ├── ATA-2026-03-20-Reuniao-Kickoff.docx
│   └── CRONO-2026-03-15-Cronograma-Projeto.xlsx
├── 📁 02_PROPOSTAS/
│   ├── PROP-2026-03-10-v1.0-Proposta-Inicial.pptx
│   ├── PROP-2026-03-15-v1.1-Proposta-Revisada.pptx
│   └── PROP-2026-03-20-v2.0-Proposta-Final.pptx
└── 📁 03_ENTREGAS/
    ├── REL-2026-03-25-Relatorio-Parcial.docx
    └── REL-2026-03-30-Relatorio-Final.docx
```

---

## Dicas Rápidas

1. **Sempre comece com data** → facilita ordenação cronológica
2. **Use números de versão** → v1.0, v1.1, v2.0
3. **Seja específico** → "Relatorio-Vendas-Marco" é melhor que "Relatorio"
4. **Evite "final"** → sempre surge uma versão "final_final"
5. **Backup primeiro** → renomear em lote pode dar errado

---

## Atalhos Úteis (Windows)

- **F2** → Renomear arquivo selecionado
- **Ctrl+C** → Copiar
- **Ctrl+X** → Recortar
- **Ctrl+V** → Colar
- **Ctrl+Z** → Desfazer
- **Ctrl+Shift+N** → Nova pasta
- **Win+E** → Explorador de arquivos

---

**Material elaborado para PTIC - 2026**  
Prof. Gustavo Villalta

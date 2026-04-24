---
layout: material
title: "Guia de Nomenclatura de Arquivos"
course_id: ptic
---

# 📄 Guia de Nomenclatura de Arquivos

Organizar arquivos não é apenas sobre "estética", é sobre **produtividade** e
**profissionalismo**. Siga estas regras em todas as suas atividades.

---

## 1. Regra de Ouro: Data Primeiro (ISO 8601)

Sempre comece nomes de arquivos que precisam de ordem cronológica com a data no
formato `AAAA-MM-DD`.

- **Certo:** `2026-03-30-Relatorio-Vendas.pdf`
- **Errado:** `Relatorio-30-03-2026.pdf` (O computador vai ordenar pelo dia 30,
  não pelo ano/mês).

---

## 2. Sem Espaços ou Caracteres Especiais

Sistemas operacionais e servidores de nuvem podem ter problemas com espaços e
acentos em links.

- **Use Hífens (`-`) ou Underscores (`_`):** `projeto-festa-junina.docx` ou
  `projeto_festa_junina.docx`.
- **Evite:** `ç`, `~`, `á`, `!`, `@`, `#`.

---

## 3. Nomes Descritivos e Curtos

O nome deve dizer o que tem dentro do arquivo sem precisar abrir, mas não deve
ser uma frase inteira.

- **Certo:** `ATA-2026-03-30-Reuniao-Diretoria.pdf`
- **Errado:** `ata_da_reuniao_que_tivemos_com_a_diretoria_na_segunda.pdf`

---

## 4. Padronização de Prefixos

Use prefixos para identificar o tipo de documento rapidamente:

- `REL-`: Relatórios
- `PLAN-`: Planilhas / Planejamento
- `ATA-`: Atas de Reunião
- `ORC-`: Orçamentos
- `DOC-`: Documentos Gerais

---

## 5. Exemplo de Hierarquia Profissional

```text
📁 Documentos_Empresa/
├── 📁 01_Administrativo/
│   ├── 📁 2026/
│   │   ├── 📄 REL-2026-01-Balanco.xlsx
│   │   └── 📄 ATA-2026-02-Reuniao.pdf
├── 📁 02_Marketing/
└── 📁 99_Arquivo_Morto/
```

---

**Lembre-se:** O atalho **F2** no Windows renomeia arquivos instantaneamente!

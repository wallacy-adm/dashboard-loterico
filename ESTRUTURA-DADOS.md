# 📊 Estrutura de Dados Excel

## 📁 **Visão Geral**

O dashboard processa um arquivo Excel (.xlsx) com **6 planilhas obrigatórias**. Cada planilha tem colunas específicas e regras de formatação.

---

## 🗂️ **Planilhas Obrigatórias**

### **1. Planilha: `vendas`**

**Descrição:** Dados de faturamento por produto, rota, ponto e mês.

**Colunas:**

| Coluna | Tipo | Obrigatória | Descrição | Exemplo |
|--------|------|-------------|-----------|---------|
| `ano` | Texto/Número | ✅ | Ano (4 dígitos) | `2026` |
| `mes` | Texto | ✅ | Mês (3 letras minúsculas) | `jan`, `fev`, `mar` |
| `rota` | Texto/Número | ✅ | Código da rota (4 dígitos) | `2201`, `2204` |
| `codigo` | Texto/Número | ✅ | Código completo (6 dígitos) | `220101`, `220822` |
| `jb` | Número | ✅ | Vendas produto JB | `15000.50` |
| `le` | Número | ✅ | Vendas produto LE | `12000.00` |
| `bg` | Número | ✅ | Vendas produto BG | `8500.75` |
| `cn` | Número | ✅ | Vendas produto CN | `3200.00` |

**Regras:**
- ✅ Meses: `jan`, `fev`, `mar`, `abr`, `mai`, `jun`, `jul`, `ago`, `set`, `out`, `nov`, `dez`
- ✅ Código formato: `RRRRPP` (4 dígitos rota + 2 dígitos ponto)
- ✅ Valores podem ser 0 (zero)
- ✅ Uma linha por código/mês/ano

**Exemplo:**
```
ano  | mes | rota | codigo | jb       | le       | bg      | cn
2026 | jan | 2201 | 220101 | 15000.50 | 12000.00 | 8500.75 | 3200.00
2026 | jan | 2201 | 220102 | 18500.00 | 14200.50 | 9100.00 | 2800.00
2026 | fev | 2201 | 220101 | 16200.00 | 11800.00 | 8200.00 | 3500.00
```

---

### **2. Planilha: `dezena`**

**Descrição:** Custos de dezena por produto, rota, ponto e mês.

**Colunas:**

| Coluna | Tipo | Obrigatória | Descrição | Exemplo |
|--------|------|-------------|-----------|---------|
| `ano` | Texto/Número | ✅ | Ano (4 dígitos) | `2026` |
| `mes` | Texto | ✅ | Mês (3 letras) | `jan` |
| `rota` | Texto/Número | ✅ | Código da rota | `2201` |
| `codigo` | Texto/Número | ✅ | Código completo | `220101` |
| `jb` | Número | ✅ | Custo dezena JB | `2500.00` |
| `le` | Número | ✅ | Custo dezena LE | `2100.00` |
| `bg` | Número | ✅ | Custo dezena BG | `1800.00` |
| `cn` | Número | ✅ | Custo dezena CN | `600.00` |

**Regras:**
- ✅ Mesma estrutura da planilha `vendas`
- ✅ Valores representam custos (positivos)
- ✅ Deve haver correspondência com dados de vendas

**Exemplo:**
```
ano  | mes | rota | codigo | jb      | le      | bg      | cn
2026 | jan | 2201 | 220101 | 2500.00 | 2100.00 | 1800.00 | 600.00
```

---

### **3-5. Planilhas: `comissao_jb`, `comissao_le`, `comissao_bg`**

**Descrição:** Comissões por produto (uma planilha para cada).

**Colunas:**

| Coluna | Tipo | Obrigatória | Descrição | Exemplo |
|--------|------|-------------|-----------|---------|
| `ano` | Texto/Número | ✅ | Ano | `2026` |
| `mes` | Texto | ✅ | Mês | `jan` |
| `rota` | Texto/Número | ✅ | Rota | `2201` |
| `codigo` | Texto/Número | ✅ | Código | `220101` |
| `comissao` | Número | ✅ | Valor da comissão | `750.00` |

**Regras:**
- ✅ `comissao_jb`: Comissões do produto JB
- ✅ `comissao_le`: Comissões do produto LE
- ✅ `comissao_bg`: Comissões do produto BG
- ❌ **Não existe** `comissao_cn` (CN nunca tem comissão!)

**Exemplo `comissao_jb`:**
```
ano  | mes | rota | codigo | comissao
2026 | jan | 2201 | 220101 | 750.00
2026 | jan | 2201 | 220102 | 925.00
```

---

### **6. Planilha: `aluguel`**

**Descrição:** Custos fixos de aluguel por ponto de venda.

**⚠️ IMPORTANTE:** Suporta 2 formatos (híbrido):

#### **Formato 1: Sem Data (Fixo)**

**Colunas:**

| Coluna | Tipo | Obrigatória | Descrição | Exemplo |
|--------|------|-------------|-----------|---------|
| `codigo` | Texto/Número | ✅ | Código do ponto | `220101` |
| `valor` | Número | ✅ | Valor mensal fixo | `500.00` |

**Regras:**
- ✅ Valor aplica-se a **todos os meses**
- ✅ Mais simples quando aluguel não muda

**Exemplo:**
```
codigo | valor
220101 | 500.00
220102 | 650.00
220822 | 480.00
```

#### **Formato 2: Com Data (Variável)**

**Colunas:**

| Coluna | Tipo | Obrigatória | Descrição | Exemplo |
|--------|------|-------------|-----------|---------|
| `ano` | Texto/Número | ✅ | Ano | `2026` |
| `mes` | Texto | ✅ | Mês | `jan` |
| `codigo` | Texto/Número | ✅ | Código | `220101` |
| `valor` | Número | ✅ | Valor daquele mês | `500.00` |

**Regras:**
- ✅ Permite aluguel diferente por mês
- ✅ Mais flexível para mudanças

**Exemplo:**
```
ano  | mes | codigo | valor
2026 | jan | 220101 | 500.00
2026 | fev | 220101 | 520.00  ← Mudou!
```

**💡 Pode misturar formatos!** O sistema detecta automaticamente.

---

## 🎯 **Regras Globais**

### **Códigos (Rota + Ponto)**

**Formato:** `RRRRPP`
- **RRRR**: 4 dígitos da rota
- **PP**: 2 dígitos do ponto

**Exemplos:**
```
220101 → Rota 2201, Ponto 01
220822 → Rota 2208, Ponto 22
220403 → Rota 2204, Ponto 03
```

### **Meses**

**Ordem cronológica obrigatória:**
```
jan, fev, mar, abr, mai, jun, jul, ago, set, out, nov, dez
```

**❌ NÃO usar:**
- Janeiro, Fevereiro (nome completo)
- 01, 02, 03 (números)
- JAN, FEV (maiúsculas)

### **Anos**

- ✅ Formato: 4 dígitos (`2026`)
- ✅ Pode ser número ou texto
- ✅ Aceita múltiplos anos

### **Valores Numéricos**

- ✅ Separador decimal: ponto (`.`)
- ✅ Sem separador de milhares
- ✅ Valores zero são válidos
- ✅ Valores negativos **não** são esperados

**Exemplos válidos:**
```
15000.50
12000
8500.75
0
```

**❌ Inválidos:**
```
15.000,50  (vírgula decimal)
12,000.50  (separador milhares)
-500       (negativo)
```

---

## 📋 **Produtos**

### **JB (Jogo Benefício)**
- ✅ Tem: Vendas, Dezena, Comissão, Aluguel
- ✅ Todos os campos aplicáveis

### **LE (Loteria Esportiva)**
- ✅ Tem: Vendas, Dezena, Comissão, Aluguel
- ✅ Todos os campos aplicáveis

### **BG (Bingo)**
- ✅ Tem: Vendas, Dezena, Comissão, Aluguel
- ✅ Todos os campos aplicáveis

### **CN (Caça-Níquel)**
- ✅ Tem: Vendas, Dezena, Aluguel
- ❌ **NUNCA** tem Comissão
- ⚠️ Não criar planilha `comissao_cn`

---

## 🔍 **Validações do Sistema**

O dashboard valida automaticamente:

### **✅ Validações que PASSAM:**
- Nome das planilhas correto
- Colunas obrigatórias presentes
- Formatos de data válidos
- Valores numéricos válidos

### **❌ Erros que BLOQUEIAM:**
- Falta de planilha obrigatória
- Nome de coluna errado
- Formato de mês inválido
- Dados não numéricos em campos numéricos

---

## 📝 **Template de Exemplo**

**Baixe:** `/exemplos/template-dados.xlsx`

**Contém:**
- ✅ Estrutura completa das 6 planilhas
- ✅ Exemplos de dados fictícios
- ✅ Comentários explicativos
- ✅ Formato correto

**Use como base** para seus próprios dados!

---

## 💡 **Dicas de Preparação**

### **1. Consolidação de Dados**

Se seus dados vêm de múltiplas fontes:

```
Sistema A → Vendas
Sistema B → Comissões
Sistema C → Aluguel
      ↓
Consolidar no Excel
      ↓
Dashboard
```

### **2. Fórmulas Excel**

Pode usar fórmulas! O dashboard lê apenas os **valores finais**.

**Exemplo:**
```excel
=SOMA(D2:D10)  ← OK! Dashboard vê o resultado
```

### **3. Formatação**

**Não afeta:**
- Cores de células
- Fontes
- Bordas
- Formatação condicional

**Afeta:**
- Nomes de colunas (devem ser exatos)
- Nomes de planilhas (devem ser exatos)
- Formato de valores (ponto decimal)

### **4. Múltiplos Períodos**

**Recomendação:** Um arquivo por ano

```
dados-2025.xlsx
dados-2026.xlsx
dados-2027.xlsx
```

**OU:** Arquivo único com todos os anos

```
dados-completo.xlsx
  └─ Vendas (2024-2026)
  └─ Dezena (2024-2026)
  └─ ...
```

---

## ⚠️ **Problemas Comuns**

### **Erro: "Planilha não encontrada"**

**Causa:** Nome da aba incorreto

**Solução:**
```
❌ Vendas   → Maiúscula
❌ vendas.  → Ponto extra
✅ vendas   → Correto
```

### **Erro: "Coluna não encontrada"**

**Causa:** Nome de coluna incorreto

**Solução:**
```
❌ Código  → Maiúscula
❌ codigo. → Ponto extra
❌ codígo  → Acento
✅ codigo  → Correto
```

### **Dados não aparecem**

**Causas possíveis:**
- Formato de mês errado (`janeiro` ≠ `jan`)
- Ano como data (`01/01/2026` ≠ `2026`)
- Valores com vírgula (`1.500,00` ≠ `1500.00`)

---

## 🧪 **Teste seu Arquivo**

**Checklist:**

- [ ] 6 planilhas presentes
- [ ] Nomes exatos (minúsculas)
- [ ] Colunas obrigatórias em cada planilha
- [ ] Meses no formato correto (`jan`, `fev`...)
- [ ] Códigos no formato `RRRRPP`
- [ ] Valores com ponto decimal
- [ ] Pelo menos 1 mês de dados

**✅ Se passou em tudo, está pronto para o dashboard!**

---

## 📞 **Precisa de Ajuda?**

- Consulte o template em `/exemplos/template-dados.xlsx`
- Veja exemplos nesta documentação
- Abra uma issue no GitHub

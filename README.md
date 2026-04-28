# 📋 Template de Dados Excel

## 🎯 **Como Usar Este Template**

Este arquivo serve como modelo para estruturar seus dados para o Dashboard Gerencial.

### **Opção 1: Criar Manualmente no Excel**

1. Abra o Microsoft Excel
2. Crie 6 planilhas (abas) com os nomes **exatos**:
   - `vendas`
   - `dezena`
   - `comissao_jb`
   - `comissao_le`
   - `comissao_bg`
   - `aluguel`

3. Em cada planilha, adicione as colunas conforme especificado abaixo

### **Opção 2: Use a Estrutura Documentada**

Consulte [ESTRUTURA-DADOS.md](../docs/ESTRUTURA-DADOS.md) para detalhes completos.

---

## 📊 **Estrutura das Planilhas**

### **Planilha: vendas**

| ano | mes | rota | codigo | jb | le | bg | cn |
|-----|-----|------|--------|----|----|----|----|
| 2026 | jan | 2201 | 220101 | 15000.50 | 12000.00 | 8500.75 | 3200.00 |
| 2026 | jan | 2201 | 220102 | 18500.00 | 14200.50 | 9100.00 | 2800.00 |

**Descrição das Colunas:**
- `ano`: Ano (4 dígitos, ex: 2026)
- `mes`: Mês (3 letras minúsculas: jan, fev, mar...)
- `rota`: Código da rota (4 dígitos)
- `codigo`: Código completo ponto (6 dígitos: RRRRPP)
- `jb`, `le`, `bg`, `cn`: Vendas de cada produto

---

### **Planilha: dezena**

| ano | mes | rota | codigo | jb | le | bg | cn |
|-----|-----|------|--------|----|----|----|----|
| 2026 | jan | 2201 | 220101 | 2500.00 | 2100.00 | 1800.00 | 600.00 |
| 2026 | jan | 2201 | 220102 | 3100.00 | 2400.00 | 2000.00 | 500.00 |

**Descrição:** Mesma estrutura de `vendas`, mas com custos de dezena.

---

### **Planilha: comissao_jb**

| ano | mes | rota | codigo | comissao |
|-----|-----|------|--------|----------|
| 2026 | jan | 2201 | 220101 | 750.00 |
| 2026 | jan | 2201 | 220102 | 925.00 |

**Descrição:** Comissões do produto JB.

---

### **Planilha: comissao_le**

| ano | mes | rota | codigo | comissao |
|-----|-----|------|--------|----------|
| 2026 | jan | 2201 | 220101 | 600.00 |
| 2026 | jan | 2201 | 220102 | 710.00 |

**Descrição:** Comissões do produto LE.

---

### **Planilha: comissao_bg**

| ano | mes | rota | codigo | comissao |
|-----|-----|------|--------|----------|
| 2026 | jan | 2201 | 220101 | 425.00 |
| 2026 | jan | 2201 | 220102 | 455.00 |

**Descrição:** Comissões do produto BG.

---

### **Planilha: aluguel**

**Opção 1 - Fixo (sem data):**

| codigo | valor |
|--------|-------|
| 220101 | 500.00 |
| 220102 | 650.00 |

**Opção 2 - Variável (com data):**

| ano | mes | codigo | valor |
|-----|-----|--------|-------|
| 2026 | jan | 220101 | 500.00 |
| 2026 | fev | 220101 | 520.00 |

**Descrição:** Custos de aluguel. Pode usar formato fixo ou variável.

---

## ⚠️ **IMPORTANTE**

### **Nomes Exatos**
- Planilhas devem ter nomes **exatamente** como especificado (minúsculas)
- Colunas devem ter nomes **exatamente** como especificado

### **Formato de Meses**
- Use **apenas** 3 letras minúsculas: `jan`, `fev`, `mar`, `abr`, `mai`, `jun`, `jul`, `ago`, `set`, `out`, `nov`, `dez`
- ❌ **NÃO** use: Janeiro, JAN, 01, 1

### **Códigos**
- Formato: `RRRRPP` (6 dígitos)
- Exemplo: `220101` = Rota 2201, Ponto 01

### **Produto CN**
- CN **nunca** tem comissão
- Não crie planilha `comissao_cn`

### **Valores**
- Use ponto (`.`) como separador decimal: `1500.50`
- ❌ **NÃO** use vírgula: ~~`1.500,50`~~
- Sem separador de milhares

---

## 📝 **Exemplo Mínimo**

Para testar o dashboard, você precisa **no mínimo**:

1. **Vendas:** 1 linha com dados de 1 ponto em 1 mês
2. **Dezena:** 1 linha correspondente
3. **Comissões JB/LE/BG:** 1 linha cada
4. **Aluguel:** 1 linha com o código do ponto

**Arquivo mínimo funcional:**
- 6 planilhas criadas ✅
- Pelo menos 1 ponto com dados completos ✅
- Dados de jan/2026 (para incluir despesas) ✅

---

## 🆘 **Precisa de Ajuda?**

- Veja documentação completa: [ESTRUTURA-DADOS.md](../docs/ESTRUTURA-DADOS.md)
- Confira exemplos de valores válidos
- Verifique nomes de planilhas e colunas

---

## ✅ **Checklist Final**

Antes de usar seu arquivo no dashboard:

- [ ] 6 planilhas com nomes corretos (minúsculas)
- [ ] Todas as colunas obrigatórias presentes
- [ ] Meses no formato `jan`, `fev`, etc.
- [ ] Códigos no formato `RRRRPP`
- [ ] Valores com ponto decimal
- [ ] Sem planilha `comissao_cn`
- [ ] Pelo menos 1 mês de dados

**Se todos os itens estão marcados, seu arquivo está pronto! 🎉**

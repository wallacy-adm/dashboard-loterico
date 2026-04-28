# 📊 DATA-STRUCTURE - Estrutura dos Dados

> Documentação completa do formato esperado das planilhas Excel processadas pelo dashboard.

---

## 📁 Visão Geral

O dashboard processa **6 planilhas Excel** distintas:

| # | Planilha | Conteúdo | Frequência |
|---|----------|----------|------------|
| 1 | `vendas` | Vendas por produto | Mensal |
| 2 | `dezena` | Despesa de dezena | Mensal |
| 3 | `comissao_jb` | Comissão JB | Mensal |
| 4 | `comissao_le` | Comissão LE | Mensal |
| 5 | `comissao_bg` | Comissão BG | Mensal |
| 6 | `aluguel` | Aluguel fixo | Sem data |

⚠️ **CN nunca tem planilha de comissão** - é uma regra de negócio fixa.

---

## 📋 Planilha 1: vendas

### Colunas Esperadas:

| Coluna  | Tipo   | Descrição                         | Exemplo  | Obrigatório |
|---------|--------|-----------------------------------|----------|-------------|
| codigo  | String | Código RRRRPP                     | 220505   | ✅ Sim      |
| rota    | String | 4 primeiros dígitos do código     | 2205     | ✅ Sim      |
| jb      | Number | Vendas do Jogo do Bicho (R$)      | 5000.00  | ✅ Sim      |
| le      | Number | Vendas da Loteria (R$)            | 3000.00  | ✅ Sim      |
| bg      | Number | Vendas do Bingo (R$)              | 2000.00  | ✅ Sim      |
| cn      | Number | Vendas do Caça-Níquel (R$)        | 1500.00  | ✅ Sim      |
| mes     | String | Mês abreviado em minúsculas       | jan      | ✅ Sim      |
| ano     | Number | Ano com 4 dígitos                 | 2026     | ✅ Sim      |

### Exemplo:

```
| codigo | rota | jb     | le     | bg     | cn     | mes | ano  |
|--------|------|--------|--------|--------|--------|-----|------|
| 220505 | 2205 | 5000.00| 3000.00| 2000.00| 1500.00| jan | 2026 |
| 220506 | 2205 | 4500.00| 2800.00| 1900.00| 1200.00| jan | 2026 |
| 220507 | 2205 | 6000.00| 3500.00| 2200.00| 1800.00| jan | 2026 |
```

### Observações:
- ✅ Valores em **Reais (BRL)** com 2 casas decimais
- ✅ Mês sempre em **minúsculas** (`jan`, não `Jan` ou `JAN`)
- ✅ Ano como **número** (2026, não "2026")
- ✅ Código como **string** (preserva zeros à esquerda)
- ⚠️ Vendas zeradas são permitidas (escondem nos filtros, mas processam)

---

## 📋 Planilha 2: dezena

### Colunas Esperadas:

| Coluna | Tipo   | Descrição                    | Exemplo | Obrigatório |
|--------|--------|------------------------------|---------|-------------|
| codigo | String | Código RRRRPP                | 220505  | ✅ Sim      |
| valor  | Number | Despesa de dezena (R$)       | 200.00  | ✅ Sim      |
| mes    | String | Mês abreviado                | jan     | ✅ Sim      |
| ano    | Number | Ano                          | 2026    | ✅ Sim      |

### Exemplo:

```
| codigo | valor  | mes | ano  |
|--------|--------|-----|------|
| 220505 | 200.00 | jan | 2026 |
| 220506 | 180.00 | jan | 2026 |
| 220507 | 220.00 | jan | 2026 |
```

---

## 📋 Planilhas 3-5: comissao_jb, comissao_le, comissao_bg

### Estrutura idêntica para os 3 produtos:

| Coluna | Tipo   | Descrição                    | Exemplo | Obrigatório |
|--------|--------|------------------------------|---------|-------------|
| codigo | String | Código RRRRPP                | 220505  | ✅ Sim      |
| valor  | Number | Valor da comissão (R$)       | 500.00  | ✅ Sim      |
| mes    | String | Mês abreviado                | jan     | ✅ Sim      |
| ano    | Number | Ano                          | 2026    | ✅ Sim      |

### Exemplo (`comissao_jb`):

```
| codigo | valor  | mes | ano  |
|--------|--------|-----|------|
| 220505 | 500.00 | jan | 2026 |
| 220506 | 450.00 | jan | 2026 |
| 220507 | 600.00 | jan | 2026 |
```

### ⚠️ IMPORTANTE: Não existe `comissao_cn`!
- CN nunca tem comissão (regra de negócio)
- Se houver planilha com esse nome, ela será **ignorada**

---

## 📋 Planilha 6: aluguel

### ⚠️ ATENÇÃO: Estrutura DIFERENTE!

Esta planilha **NÃO TEM** colunas de mês/ano. O aluguel é fixo por código.

### Colunas Esperadas:

| Coluna | Tipo   | Descrição                    | Exemplo | Obrigatório |
|--------|--------|------------------------------|---------|-------------|
| codigo | String | Código RRRRPP                | 220505  | ✅ Sim      |
| valor  | Number | Aluguel mensal fixo (R$)     | 100.00  | ✅ Sim      |

### Exemplo:

```
| codigo | valor  |
|--------|--------|
| 220505 | 100.00 |
| 220506 | 100.00 |
| 220507 |  80.00 |
```

### Comportamento:
- O mesmo valor se aplica a **todos os meses** em que o código tem vendas
- Se um código não estiver listado em `aluguel`, o valor é considerado **0**
- Não é necessário ter aluguel para todos os códigos

---

## 🔄 Fluxo de Processamento

```
1. Usuário faz upload do arquivo .xlsx
   ↓
2. ExcelJS lê o workbook
   ↓
3. Para cada planilha esperada:
   ├── Validar nome
   ├── Validar colunas
   ├── Processar linhas
   └── Armazenar em state.dados[nome]
   ↓
4. Validar consistência geral
   ↓
5. Renderizar dashboard
```

---

## 🛡️ Validações Aplicadas

### Validações de Estrutura:

```javascript
// Para cada planilha:
1. Verificar se a planilha existe no workbook
2. Verificar se tem pelo menos 2 linhas (cabeçalho + 1 dado)
3. Verificar se as colunas obrigatórias existem
4. Verificar tipos de dados
```

### Validações de Dados:

```javascript
// Para cada linha:
1. codigo é string de 6 dígitos? (RRRRPP)
2. valor é número positivo?
3. mes é um dos 12 valores válidos?
4. ano é número de 4 dígitos?
```

### Comportamento em caso de erro:

- **Erro fatal:** Planilha obrigatória ausente → Exibe mensagem de erro
- **Erro de linha:** Linha com dado inválido → Pula a linha, registra log
- **Aviso:** Coluna esperada vazia → Considera valor 0

---

## 📊 Como os Dados São Armazenados

### State Estruturado:

```javascript
state.dados = {
    vendas: [
        { codigo: '220505', rota: '2205', jb: 5000, le: 3000, 
          bg: 2000, cn: 1500, mes: 'jan', ano: 2026 },
        // ... mais registros
    ],
    
    dezena: [
        { codigo: '220505', valor: 200, mes: 'jan', ano: 2026 },
        // ... mais registros
    ],
    
    comissao: {
        jb: [
            { codigo: '220505', valor: 500, mes: 'jan', ano: 2026 },
            // ...
        ],
        le: [ /* similar */ ],
        bg: [ /* similar */ ]
    },
    
    aluguel: [
        { codigo: '220505', valor: 100 }, // Sem mes/ano!
        // ...
    ]
};
```

---

## 🔗 Cruzamento de Dados

### Como o dashboard cruza informações:

```javascript
// Para um registro de venda específico:
const venda = { codigo: '220505', mes: 'jan', ano: 2026, jb: 5000, ... };

// Buscar comissão correspondente:
const comissaoJb = state.dados.comissao.jb.find(c => 
    c.codigo === venda.codigo && 
    c.mes === venda.mes && 
    c.ano === venda.ano
);

// Buscar dezena correspondente:
const dezena = state.dados.dezena.find(d => 
    d.codigo === venda.codigo && 
    d.mes === venda.mes && 
    d.ano === venda.ano
);

// Buscar aluguel (sem filtrar por mes/ano!):
const aluguel = state.dados.aluguel.find(a => 
    a.codigo === venda.codigo
);
```

---

## 📋 Exemplo Completo

### Dado de entrada (vendas):
```
codigo: 220505 | rota: 2205 | jb: 5000 | le: 3000 | bg: 2000 | cn: 1500 | mes: jan | ano: 2026
```

### Dado de comissão (jb):
```
codigo: 220505 | valor: 500 | mes: jan | ano: 2026
```

### Dado de comissão (le):
```
codigo: 220505 | valor: 300 | mes: jan | ano: 2026
```

### Dado de comissão (bg):
```
codigo: 220505 | valor: 200 | mes: jan | ano: 2026
```

### Dado de dezena:
```
codigo: 220505 | valor: 200 | mes: jan | ano: 2026
```

### Dado de aluguel:
```
codigo: 220505 | valor: 100
```

### Cálculos derivados:

```javascript
totalVendas = 5000 + 3000 + 2000 + 1500 = R$ 11.500,00

comissaoTotal = 500 + 300 + 200 = R$ 1.000,00
// CN não entra!

despesaTotal = 1000 + 200 + 100 = R$ 1.300,00
// comissão + dezena + aluguel

custoPercentual = (1300 / 11500) * 100 = 11,30%
// Status: 🟢 Verde (Ideal, < 25%)
```

---

## 🚨 Erros Comuns

### Erro 1: Mês com letra maiúscula
```
❌ "Jan", "JAN", "Janeiro"
✅ "jan"
```

### Erro 2: Código com menos de 6 dígitos
```
❌ "5", "05", "2205"
✅ "220505"
```

### Erro 3: Aluguel com coluna de data
```
❌ aluguel.xlsx tem colunas: codigo, valor, mes, ano
✅ aluguel.xlsx tem colunas: codigo, valor
```

### Erro 4: Existir planilha "comissao_cn"
```
❌ Planilha "comissao_cn" no workbook
✅ Apenas comissao_jb, comissao_le, comissao_bg
```

### Erro 5: Valor com vírgula em vez de ponto
```
❌ "5.000,00" (formato brasileiro como string)
✅ 5000.00 (número)
```

---

## 🔧 Como Adicionar Novo Tipo de Dado

Se precisar adicionar uma nova planilha (ex: "premiacao"):

### Passos:

1. **Definir estrutura:**
   - Quais colunas?
   - Quais validações?

2. **Atualizar este documento** (DATA-STRUCTURE.md)

3. **Atualizar processamento:**
   ```javascript
   // Em processarPlanilha()
   if (sheet.name === 'premiacao') {
       state.dados.premiacao = processarPremiacao(sheet);
   }
   ```

4. **Atualizar regras de negócio** (BUSINESS-RULES.md)

5. **Atualizar versão** (CHANGELOG.md)

---

**Última atualização:** 2026-04-28 (v1.1.0)

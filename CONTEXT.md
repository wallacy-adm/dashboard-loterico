# 📋 BUSINESS-RULES - Regras de Negócio

> Documento completo de TODAS as regras de negócio do projeto. Crítico para qualquer modificação.

---

## 🎯 Domínio do Negócio

**Setor:** Análise de vendas e despesas para negócios de jogos populares
**Produtos:** JB, LE, BG, CN
**Estrutura:** Multi-rota com pontos de venda

---

## 🔑 Regras Críticas (NUNCA VIOLAR)

### REGRA 1: CN não tem comissão

**Descrição:** O produto CN (Caça-Níquel) **JAMAIS** deve ter cálculo de comissão.

**Onde aplica:**
- Aba Despesas (não somar comissão de CN)
- Aba Comparativo (variação de comissão CN sempre 0)
- Cards de breakdown
- Tabelas detalhadas
- Gráficos de despesas

**Implementação:**
```javascript
// ✅ CORRETO
function calcularComissao(produto, valor) {
    if (produto === 'cn') return 0; // CN nunca tem comissão
    return valor * percentualComissao;
}

// ❌ ERRADO
function calcularComissao(produto, valor) {
    return valor * percentualComissao; // Aplica em todos
}
```

**Impacto se violado:** Distorção total dos cálculos de despesa, cards crítico/atenção/ideal incorretos.

---

### REGRA 2: Formato de Código RRRRPP

**Descrição:** Todo código segue formato de 6 dígitos: 4 da rota + 2 do ponto.

**Estrutura:**
```
220505
├── 2205 = Rota
└──   05 = Ponto
```

**Validações:**
- Sempre 6 dígitos exatos
- Primeiros 4 = rota
- Últimos 2 = ponto
- Números puros (sem letras/caracteres)

**Exibição:**
```javascript
// ✅ CORRETO - Mostra código completo
<td>{codigo}</td> // "220505"

// ❌ ERRADO - Mostra só os últimos 2 dígitos
<td>{codigo.slice(-2)}</td> // "05"
```

**Filtragem:**
```javascript
// Filtrar por rota
dados.filter(d => d.codigo.slice(0, 4) === rotaSelecionada);

// Filtrar por ponto (código completo)
dados.filter(d => d.codigo === codigoSelecionado);
```

---

### REGRA 3: Aluguel é fixo por código

**Descrição:** O aluguel é um custo fixo associado a cada código (RRRRPP), **sem variar por mês**.

**Estrutura da planilha aluguel:**
```
codigo  | valor
220505  | 100
220506  | 100
220507  | 80
```

⚠️ **NÃO TEM coluna de mês/ano!**

**Aplicação:**
- O mesmo valor de aluguel se aplica a TODOS os meses
- Se o código existir nas vendas em jan, fev, mar... aluguel é cobrado em todos

**Implementação:**
```javascript
// ✅ CORRETO
function getAluguel(codigo, mes, ano) {
    const aluguelData = state.dados.aluguel.find(a => a.codigo === codigo);
    return aluguelData ? aluguelData.valor : 0;
    // Não filtra por mes/ano - é fixo!
}

// ❌ ERRADO
function getAluguel(codigo, mes, ano) {
    return state.dados.aluguel.find(a => 
        a.codigo === codigo && a.mes === mes && a.ano === ano
    );
}
```

---

### REGRA 4: Chave única para Despesas

**Descrição:** Toda despesa (comissão, dezena, aluguel) é identificada pela combinação `codigo-mes-ano`.

**Formato:**
```
{codigo}-{mes}-{ano}
Exemplo: "220505-jan-2026"
```

**Uso:**
```javascript
// Agrupar despesas
const chave = `${codigo}-${mes}-${ano}`;
despesasAgrupadas[chave] = {
    comissao: ...,
    dezena: ...,
    aluguel: ...
};
```

**Por quê?**
- Garante unicidade
- Permite cruzar dados de múltiplas planilhas
- Facilita cálculos de período

---

### REGRA 5: Despesas a partir de Jan/2026

**Descrição:** Dados de despesas só estão disponíveis a partir de **Janeiro/2026**.

**Implicações:**
- Aba Comparativo: Períodos < 2026 não têm dados de despesa
- Mostrar aviso/filtro automático para excluir períodos sem dados
- Cards de despesa devem mostrar "—" para períodos antes de 2026

**Implementação:**
```javascript
// ✅ CORRETO
function temDespesas(ano, mes) {
    if (ano < 2026) return false;
    if (ano === 2026 && mes < 'jan') return false;
    return true;
}

// Aba Comparativo
if (!temDespesas(filtros.anoA, filtros.mesA)) {
    mostrarAviso('Período A não tem dados de despesa. Selecione período >= jan/2026');
    return;
}
```

---

### REGRA 6: Thresholds de Custo Percentual

**Descrição:** Custo percentual = (Despesas / Vendas) × 100. Classificação por faixa:

| Faixa       | Cor        | Status      | Significado                    |
|-------------|------------|-------------|--------------------------------|
| < 25%       | 🟢 Verde   | **Ideal**   | Operação saudável              |
| 25% - 35%   | 🟡 Amarelo | **Atenção** | Margem apertada                |
| > 35%       | 🔴 Vermelho| **Crítico** | Operação no prejuízo/risco     |

**Implementação:**
```javascript
function statusCusto(percentual) {
    if (percentual < 25)   return { cor: 'verde',    label: 'Ideal' };
    if (percentual <= 35)  return { cor: 'amarelo',  label: 'Atenção' };
    return                       { cor: 'vermelho', label: 'Crítico' };
}
```

**⚠️ Importante:** Cards de Status (Ideal/Atenção/Crítico) **DEVEM** corresponder exatamente às tabelas. Não pode haver divergência de cálculo.

---

### REGRA 7: Cores por Sinal Matemático

**Descrição:** Cores de variação seguem o **sinal matemático**, não a semântica de negócio.

| Valor       | Cor        |
|-------------|------------|
| Negativo (-)| 🔴 Vermelho|
| Positivo (+)| 🟢 Verde   |
| Zero (0)    | ⚪ Cinza   |

**Implementação:**
```javascript
// ✅ CORRETO
const cor = valor < 0 ? 'red' : valor > 0 ? 'green' : 'gray';

// ❌ ERRADO (semântica de negócio)
// "Despesa caiu = é bom = verde"
const cor = (tipoMetrica === 'despesa' && valor < 0) ? 'green' : 'red';
```

**Por quê?**
- Consistência visual
- Padrão financeiro internacional
- Evita confusão (usuário sempre sabe o que vermelho significa)

**Exemplo de aplicação:**
```
Vendas variaram -10% → 🔴 Vermelho (caiu)
Vendas variaram +15% → 🟢 Verde (subiu)
Despesas variaram -5% → 🔴 Vermelho (caiu, mesmo que seja "bom")
Despesas variaram +20% → 🟢 Verde (subiu)
```

⚠️ **Sim, pode parecer estranho que despesa caindo seja vermelho.** Mas é consistente: cor = sinal matemático.

---

### REGRA 8: Meses em Ordem Cronológica

**Descrição:** Meses **SEMPRE** em ordem cronológica, não alfabética.

**Ordem correta:**
```javascript
['jan', 'fev', 'mar', 'abr', 'mai', 'jun', 
 'jul', 'ago', 'set', 'out', 'nov', 'dez']
```

**Onde aplicar:**
- Dropdowns de seleção de mês
- Eixo X de gráficos
- Tabelas com colunas mensais
- Comparativos entre períodos

**Implementação:**
```javascript
const ORDEM_MESES = [
    'jan', 'fev', 'mar', 'abr', 'mai', 'jun',
    'jul', 'ago', 'set', 'out', 'nov', 'dez'
];

// Ordenar dados por mês
dados.sort((a, b) => {
    const idxA = ORDEM_MESES.indexOf(a.mes);
    const idxB = ORDEM_MESES.indexOf(b.mes);
    return idxA - idxB;
});
```

---

## 🎨 Regras Visuais

### REGRA 9: Cards Empilhados Verticalmente

**Descrição:** Cards na aba Comparativo devem ficar empilhados verticalmente.

**Implementação:**
```html
<!-- ✅ CORRETO -->
<div class="space-y-3">
    <div class="card">Card 1</div>
    <div class="card">Card 2</div>
</div>

<!-- ❌ ERRADO -->
<div class="grid grid-cols-2 gap-4">
    <div class="card">Card 1</div>
    <div class="card">Card 2</div>
</div>
```

**Por quê?**
- Melhor leitura sequencial
- Responsividade mobile
- Decisão visual do Wallacy

---

### REGRA 10: Filtro de Produto Afeta Tudo

**Descrição:** Quando o filtro de produto é alterado, **TODOS** os elementos devem atualizar.

**O que deve atualizar:**
- ✅ Cards de métricas
- ✅ Tabelas detalhadas
- ✅ Gráficos
- ✅ Cards de status
- ✅ Totais e subtotais

**Comportamento:**
```javascript
// Ao mudar filtro de produto:
state.filtros.vendas.produto = 'jb';
render(); // Re-renderiza TUDO

// Resultado: Todos os elementos refletem só dados de JB
```

---

### REGRA 11: Hide Zero Sales Records

**Descrição:** Quando filtro de produto está ativo, registros com 0 vendas desse produto devem ser **ocultados**.

**Implementação:**
```javascript
// Filtrar registros com vendas > 0 do produto
const dadosFiltrados = dados.filter(d => {
    if (filtros.produto === 'todos') return true;
    return (d[filtros.produto] || 0) > 0;
});
```

**Onde aplicar:**
- Tabela detalhada de vendas
- Dropdown de pontos disponíveis
- Cards de pontos ativos

---

## 📊 Regras de Cálculo

### Cálculo: Total de Vendas
```javascript
total = jb + le + bg + cn
```

### Cálculo: Comissão Total
```javascript
// Importante: CN não tem comissão!
comissaoTotal = comissao_jb + comissao_le + comissao_bg
// CN não entra!
```

### Cálculo: Despesa Total
```javascript
despesaTotal = comissaoTotal + dezena + aluguel
```

### Cálculo: Custo Percentual
```javascript
custoPercentual = (despesaTotal / totalVendas) * 100
```

### Cálculo: Variação Percentual
```javascript
variacao = ((valorB - valorA) / valorA) * 100
// Trata divisão por zero
if (valorA === 0) variacao = valorB > 0 ? 100 : 0;
```

### Cálculo: Variação Absoluta
```javascript
variacaoAbsoluta = valorB - valorA
```

---

## 🚨 Cenários Especiais

### Cenário 1: Produto Único Selecionado
```
Filtro: Produto = JB

Comportamento:
- Mostra apenas vendas de JB
- Mostra apenas comissão de JB
- Pontos sem vendas de JB são ocultados
- Cards refletem apenas valores de JB
```

### Cenário 2: Período Sem Despesas (< 2026)
```
Filtro: Mês A = dez/2025

Comportamento:
- Aba Comparativo bloqueia análise
- Mostra mensagem: "Selecione período >= jan/2026"
- Filtros permanecem visíveis (não trava UI)
- Aba Vendas funciona normalmente
```

### Cenário 3: Código Sem Aluguel
```
Vendas tem código 220505 mas aluguel não tem

Comportamento:
- Aluguel = 0 para esse código
- Não é erro, é dado faltante
- Mostra normalmente, só com aluguel zerado
```

### Cenário 4: Valor Zero
```
Vendas de produto X = 0

Comportamento:
- Esconde nas tabelas (se filtro de produto X ativo)
- Mostra "—" ou "R$ 0,00" se filtro = todos
- Não calcula percentuais (evita divisão por zero)
```

---

## 📝 Glossário de Termos

| Termo | Definição |
|-------|-----------|
| **Rota** | Conjunto de pontos de venda em uma região (4 dígitos) |
| **Ponto** | Local específico de venda (2 dígitos) |
| **Código** | Identificador completo do ponto (RRRRPP, 6 dígitos) |
| **Comissão** | Valor pago ao operador do ponto |
| **Dezena** | Despesa relacionada a sorteios/dezenas premiadas |
| **Aluguel** | Custo fixo do ponto de venda |
| **Custo %** | Percentual de despesa sobre vendas |
| **Ideal/Atenção/Crítico** | Status do custo percentual (verde/amarelo/vermelho) |

---

## ⚠️ Validações Obrigatórias

Toda nova funcionalidade DEVE validar:

- [ ] CN não tem comissão? (REGRA 1)
- [ ] Código RRRRPP sempre 6 dígitos? (REGRA 2)
- [ ] Aluguel não filtra por mês/ano? (REGRA 3)
- [ ] Chave correta para despesas? (REGRA 4)
- [ ] Período >= jan/2026 para despesas? (REGRA 5)
- [ ] Thresholds 25%/35% corretos? (REGRA 6)
- [ ] Cores por sinal matemático? (REGRA 7)
- [ ] Meses em ordem cronológica? (REGRA 8)
- [ ] Filtro produto atualiza tudo? (REGRA 10)
- [ ] Esconde registros com vendas zero? (REGRA 11)

---

**Última atualização:** 2026-04-28 (v1.1.0)

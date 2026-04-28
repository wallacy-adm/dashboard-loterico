# 📊 FUNCIONALIDADES - Detalhes de Cada Aba

> Descrição completa de cada aba do dashboard, suas funcionalidades, filtros e visualizações.

---

## 🎯 Visão Geral

O dashboard tem **4 abas principais**, cada uma com propósito específico:

| Aba | Propósito | Quando Usar |
|-----|-----------|-------------|
| 💰 **Vendas** | Visualização detalhada de vendas | Análise diária/mensal |
| 💸 **Despesas** | Análise de custo percentual | Controle de margens |
| ⚖️ **Comparativo** | Comparar 2 períodos | Análise mensal/anual |
| 📈 **Evolução** | Tendência temporal | Identificar padrões |

---

## 💰 Aba 1: Vendas

### Propósito:
Visualizar vendas detalhadas por produto, ponto e período.

### Filtros Disponíveis:

| Filtro | Tipo | Descrição |
|--------|------|-----------|
| **Ano** | Dropdown | Seleciona ano específico |
| **Mês** | Dropdown | Seleciona mês específico |
| **Rota** | Dropdown | Filtra por rota (4 dígitos) |
| **Ponto** | Dropdown | Filtra por ponto específico |
| **Produto** | Dropdown | JB, LE, BG, CN ou Todos |

### Cards de Métricas:

#### Total de Vendas
- Soma total no período filtrado
- Atualiza com filtros

#### Ticket Médio
- Vendas total ÷ Quantidade de pontos
- Indicador de performance individual

#### Pontos Ativos
- Quantos pontos tiveram vendas no período
- Auxilia na análise de cobertura

### Tabela Detalhada:

```
| Código | Rota | JB | LE | BG | CN | Total |
|--------|------|----|----|----|----|----|
| 220505 | 2205| 5k | 3k | 2k | 1.5k| 11.5k|
| 220506 | 2205| 4.5k| 2.8k| 1.9k| 1.2k| 10.4k|
```

**Comportamento:**
- Ordenação por código (padrão)
- Esconde linhas com 0 do produto filtrado
- Total atualizado dinamicamente

### Gráfico:

**Tipo:** Pizza/Donut
**Mostra:** Distribuição de vendas por produto
**Cores:**
- JB: Verde
- LE: Azul
- BG: Amarelo
- CN: Vermelho

---

## 💸 Aba 2: Despesas

### Propósito:
Analisar despesas e calcular custo percentual sobre vendas.

### Filtros:
- Mesmos da aba Vendas (sincronizados)

### Componentes de Despesa:

#### 1. Comissão
- Soma de comissão_jb + comissao_le + comissao_bg
- ⚠️ CN nunca entra!

#### 2. Dezena
- Despesa de dezena por código/período

#### 3. Aluguel
- Custo fixo por código (sem mês/ano)

### Cards de Status:

#### Card Ideal (🟢 Verde)
- Mostra quantos pontos têm custo < 25%
- "Operação saudável"

#### Card Atenção (🟡 Amarelo)
- Mostra quantos pontos têm custo entre 25% e 35%
- "Margem apertada"

#### Card Crítico (🔴 Vermelho)
- Mostra quantos pontos têm custo > 35%
- "Risco de prejuízo!"

### Tabela Detalhada:

```
| Código | Vendas | Comissão | Dezena | Aluguel | Total Desp. | Custo % | Status |
|--------|--------|----------|--------|---------|-------------|---------|--------|
| 220505 | 11.5k  | 1k       | 200    | 100     | 1.3k        | 11.3%   | 🟢 Ideal|
| 220506 | 10.4k  | 950      | 180    | 100     | 1.23k       | 11.8%   | 🟢 Ideal|
| 220507 | 13.5k  | 1.1k     | 220    | 80      | 1.4k        | 10.4%   | 🟢 Ideal|
```

### Gráfico:

**Tipo:** Barras horizontais
**Mostra:** Composição de despesas por componente
**Permite:** Identificar qual despesa pesa mais

---

## ⚖️ Aba 3: Comparativo

### Propósito:
Comparar performance entre dois períodos.

### Filtros:

#### Período A:
- Ano A
- Mês A

#### Período B:
- Ano B
- Mês B

### Restrição Importante:
- ⚠️ Apenas períodos **>= jan/2026**
- Períodos anteriores: filtros visíveis mas análise bloqueada

### Cards de Período:

#### Card Período A
```
┌─────────────────────────┐
│ Período A: jan/2026     │
│                          │
│ Vendas: R$ 100.000      │
│ Comissão: R$ 8.000      │
│ Dezena: R$ 2.000        │
│ Aluguel: R$ 500         │
│ Despesa Total: R$ 10.500│
│ Custo %: 10.5%          │
└─────────────────────────┘
```

#### Card Período B
- Mesma estrutura para período B

### Card Variação Total:

```
┌─────────────────────────┐
│ Variação Total          │
│                          │
│ Vendas: +15% 🟢         │
│ Despesas: +5% 🟢        │
│ Custo %: -8% 🔴         │
└─────────────────────────┘
```

⚠️ **Lembre:** Cor por sinal matemático (negativo=vermelho, positivo=verde)

### Variação por Componente:

Cards individuais para cada métrica:
- Variação de Vendas
- Variação de Comissão
- Variação de Dezena
- Variação de Aluguel
- Variação de Custo %

### Gráfico Comparativo:

**Tipo:** Barras agrupadas
**Mostra:** Período A vs B lado a lado
**Eixo X:** Componentes (vendas, comissão, dezena, etc.)
**Eixo Y:** Valor em R$

---

## 📈 Aba 4: Evolução

### Propósito:
Análise temporal multi-período para identificar tendências.

### Filtros:

#### Período (Range):
- **De:** Ano início + Mês início
- **Até:** Ano fim + Mês fim

#### Filtros Adicionais:
- Produto (JB/LE/BG/CN/Todos)
- Rota
- Ponto
- Mostrar Despesas (toggle)
- **Mostrar Todos os Pontos** (toggle)

### Filtro Dinâmico de Pontos:

⚠️ **Funcionalidade NOVA (v1.1.0):**

O dropdown "Ponto" mostra **apenas pontos com vendas > 0** do produto selecionado.

**Antes:**
```
Produto: CN
Pontos disponíveis: 220505, 220506, 220507, 220508, 220509, 220510... (todos)
```

**Depois:**
```
Produto: CN
Pontos disponíveis: 220505, 220507, 220520 (apenas com vendas de CN > 0)
```

### Cards de Métricas:

#### Card Período Inicial
- Valor de vendas no primeiro período
- Mostra label do período (ex: "jan/2026")

#### Card Período Final
- Valor de vendas no último período
- Mostra label do período

#### Card Variação Total
- (Final - Inicial) / Inicial × 100
- Cor por sinal matemático

#### Card Pico Máximo
- Maior valor no período
- Mostra qual mês foi o pico

#### Card Pico Mínimo
- Menor valor no período
- Mostra qual mês foi o vale

### Gráfico Evolução:

#### Modo Padrão (Toggle OFF):
- 1 linha agregada (roxa)
- Linha de despesas opcional (vermelha)

#### Modo Multi-Pontos (Toggle ON):
⚠️ **Funcionalidade NOVA (v1.1.0):**

**Gráfico Misto:**
```
Barras coloridas (top 10 pontos) + Linha tracejada (TOTAL)
```

**Características:**
- Cada ponto = 1 cor (10 cores na paleta)
- Linha roxa tracejada = TOTAL geral
- Legenda customizada à esquerda
- Click na legenda = mostrar/ocultar dataset
- Limita a top 10 pontos (por vendas totais)

**Por que essa combinação?**
- Detalhe individual (barras)
- Visão macro (linha total)
- Comparação ponto vs total
- Zero confusão visual

### Eixos do Gráfico:

**Eixo X:** Períodos em ordem cronológica (jan/26, fev/26, mar/26...)
**Eixo Y:** Valor em R$ (formato 0k, 10k, 20k...)

### Interatividade:

- **Hover:** Tooltip com valor exato
- **Legenda:** Click para mostrar/ocultar
- **Zoom:** Não disponível (manter simples)

---

## 🔄 Funcionalidades Compartilhadas

### Filtros Sincronizados

Quando você muda um filtro em uma aba, ele permanece ao trocar de aba:
- Vendas → Despesas: filtros de período/produto mantidos
- Não sincroniza: filtros específicos (ex: range de Evolução)

### Atualização Dinâmica

Toda mudança de filtro:
1. Atualiza state
2. Re-renderiza a aba ativa
3. Recalcula totais
4. Atualiza gráficos

### Tratamento de Dados Ausentes

- Códigos sem aluguel: aluguel = 0
- Períodos sem comissão: comissão = 0
- Produtos com vendas zero: ocultados (se filtro produto ativo)
- CN com comissão: ignorado (regra de negócio)

---

## 📊 Casos de Uso Comuns

### Caso 1: Análise Mensal
**Objetivo:** Avaliar performance do mês.

**Passos:**
1. Aba Vendas → filtrar mês/ano
2. Aba Despesas → mesmo mês, ver custos
3. Identificar pontos críticos
4. Tomar decisões

### Caso 2: Comparar Meses
**Objetivo:** Saber se este mês foi melhor que o anterior.

**Passos:**
1. Aba Comparativo
2. Período A: mês anterior
3. Período B: mês atual
4. Analisar variações

### Caso 3: Identificar Tendências
**Objetivo:** Ver evolução nos últimos meses.

**Passos:**
1. Aba Evolução
2. Selecionar range (últimos 6 meses)
3. Ativar "Mostrar Todos os Pontos"
4. Identificar pontos em crescimento/queda

### Caso 4: Investigar Ponto Específico
**Objetivo:** Por que ponto X está com problemas?

**Passos:**
1. Aba Vendas → filtrar ponto X
2. Ver histórico de vendas
3. Aba Despesas → mesmo ponto
4. Comparar com média
5. Aba Evolução → tendência do ponto

---

## 💡 Dicas de Uso Avançado

### Dica 1: Use Filtros Combinados
Combine filtros para análises específicas:
- Produto + Rota = "Performance de JB na Rota 2205"
- Produto + Ponto = "Histórico de CN no ponto 220505"

### Dica 2: Análise de Outliers
Na Evolução:
- Pico máximo muito acima da média? Investigar!
- Pico mínimo muito abaixo? Algo errado?
- Variação muito alta? Operação inconsistente.

### Dica 3: Custo Percentual
- < 15%: Excepcional
- 15-25%: Saudável
- 25-35%: Atenção
- > 35%: Ação imediata!

### Dica 4: Ponto vs Total
Na Evolução com toggle ON:
- Ponto sempre acima da linha total = star performer
- Ponto sempre abaixo = candidato a revisão

---

**Última atualização:** 2026-04-28 (v1.1.0)

# ⚙️ Funcionalidades Detalhadas

## 🎯 **Visão Geral das 4 Abas**

```
┌─────────────┬─────────────┬──────────────┬─────────────┐
│   VENDAS    │  DESPESAS   │ COMPARATIVO  │  EVOLUÇÃO   │
├─────────────┼─────────────┼──────────────┼─────────────┤
│ Análise de  │ Breakdown   │ Compara 2    │ Análise     │
│ faturamento │ custos      │ períodos     │ temporal    │
└─────────────┴─────────────┴──────────────┴─────────────┘
```

---

## 📈 **ABA 1: VENDAS**

### **Objetivo**
Análise completa de faturamento por produto, rota e ponto de venda.

### **Filtros Disponíveis**

| Filtro | Opções | Descrição |
|--------|--------|-----------|
| **Ano** | Todos, 2024, 2025, 2026... | Filtra por ano |
| **Mês** | Todos, jan, fev, mar... | Filtra por mês (ordem cronológica) |
| **Produto** | TODOS, JB, LE, BG, CN | Filtra por produto específico |
| **Rota** | Todas, 2201, 2204... | Filtra por rota |
| **Ponto** | Todos, 220101, 220822... | Filtra por ponto |

### **4 Tipos de Visualização**

#### **1. Geral**

**Cards exibidos:**
- 💰 **Vendas Totais**: Soma de todos produtos
- 🎯 **Produto de Maior Venda**: Qual produto vendeu mais
- 🏆 **Melhor Rota**: Rota com maior faturamento
- ⭐ **Melhor Ponto**: Ponto com maior faturamento

**Tabela:**
- Lista todos os pontos com vendas por produto
- Colunas: Código, Rota, JB, LE, BG, CN, Total
- Ordenação: Maior → Menor total

#### **2. Por Produto**

**Cards:**
- 4 cards com vendas de cada produto (JB, LE, BG, CN)
- Percentual sobre total

**Tabela:**
- Ranking de pontos por produto selecionado
- Destaque: 🥇 Melhor, 🥈 2º, 🥉 3º

#### **3. Por Rota**

**Cards:**
- Card para cada rota com total de vendas

**Tabela:**
- Detalhamento de pontos por rota
- Agrupado por rota

#### **4. Por Ponto**

**Tabela:**
- Lista detalhada de todos os pontos
- Vendas por produto + total
- Código completo (RRRRPP)

---

## 💰 **ABA 2: DESPESAS**

### **Objetivo**
Análise de custos com breakdown detalhado: Comissão + Dezena + Aluguel.

### **Filtros Disponíveis**

| Filtro | Opções | Descrição |
|--------|--------|-----------|
| **Ano** | Todos, 2026... | Apenas anos com despesas |
| **Mês** | Todos, jan, fev... | Mês específico |
| **Rota** | Todas, 2201... | Filtra por rota |
| **Ponto** | Todos, 220101... | Filtra por ponto |
| **Produto** | TODOS, JB, LE, BG | Filtra por produto (CN não tem comissão) |

### **Toggle "Excluir Comissões"**

**Ativo (checked):**
- Despesas = Dezena + Aluguel
- Comissão **não** entra no cálculo
- % de custo recalculado sem comissão

**Inativo (unchecked):**
- Despesas = Comissão + Dezena + Aluguel
- Cálculo normal

**Exemplo:**
```
Vendas: R$ 100.000
Comissão: R$ 5.000
Dezena: R$ 15.000
Aluguel: R$ 2.500

COM comissão:
  Despesas = R$ 22.500
  Custo % = 22,5%

SEM comissão:
  Despesas = R$ 17.500
  Custo % = 17,5%
```

### **Cards Principais**

**💰 Vendas:**
- Valor total de vendas
- Breakdown %: Comissão, Dezena, Aluguel

**💸 Despesas:**
- Valor total de despesas
- Breakdown detalhado com valores

**🎯 Custo %:**
- Percentual de custo sobre vendas
- Status: ✅ Ideal, ⚠️ Atenção, 🆘 Crítico

**📊 Status:**
- Ideal: `XX` pts com custo <25%
- Atenção: `XX` pts com custo 25-35%
- Crítico: `XX` pts com custo >35%

### **Thresholds de Custo**

| Status | % Custo | Cor | Descrição |
|--------|---------|-----|-----------|
| ✅ Ideal | < 25% | Verde | Operação saudável |
| ⚠️ Atenção | 25% - 35% | Amarelo | Atenção necessária |
| 🆘 Crítico | > 35% | Vermelho | Intervenção urgente |

### **TOP 5 Rankings**

**TOP 5 Melhor Custo %:**
- Pontos com menor % de custo
- Indicador de eficiência

**TOP 5 Maior Despesa R$:**
- Pontos com maior despesa absoluta
- Não considera vendas

### **Tabela Detalhada**

**Colunas:**
- Código
- Rota
- Vendas
- Despesas (breakdown: Comissão, Dezena, Aluguel)
- Custo %
- Status

**Cores:**
- Linha verde: Custo ideal
- Linha amarela: Atenção
- Linha vermelha: Crítico

---

## 🔄 **ABA 3: COMPARATIVO**

### **Objetivo**
Comparar dois períodos (A vs B) para identificar variação de performance.

### **Seleção de Períodos**

**Período A:**
- Ano (2024, 2025, 2026...)
- Mês (jan, fev, mar...)

**Período B:**
- Ano (2024, 2025, 2026...)
- Mês (jan, fev, mar...)

**💡 Exemplo:** jan/2026 vs fev/2026

### **Toggle Vendas / Despesas**

**Vendas:**
- Compara faturamento entre períodos
- Disponível para todos os anos

**Despesas:**
- Compara custos entre períodos
- ⚠️ **Apenas para períodos ≥ 2026**
- Mostra breakdown de componentes

### **Filtros Contextuais**

| Filtro | Descrição |
|--------|-----------|
| **Tipo** | Geral, Por Produto, Por Rota, Por Ponto |
| **Produto** | Todos, JB, LE, BG, CN |
| **Rota** | Todas, 2201, 2204... |
| **Ponto** | Todos, 220101... |

**💡 Filtros são dinâmicos:** Apenas opções com dados nos períodos A e B aparecem.

### **Visualização: Tipo Geral**

**Layout:**
```
┌────────────────────────────┐
│   Card Principal           │
│   Redução/Crescimento      │
│   -6,48% ou +12,5%        │
└────────────────────────────┘

┌──────────┐  ┌───────────────┐  ┌──────────┐
│Período A │  │Var. Component.│  │Período B │
│R$ 93.152 │  │💵 -R$ 3.736   │  │R$ 87.118 │
│          │  │📦 -R$ 2.446   │  │          │
│jan/2026  │  │🏠 +R$ 150     │  │fev/2026  │
└──────────┘  └───────────────┘  └──────────┘
```

**Cards Período A e B (Despesas):**
- Valor total
- Breakdown: Comissão, Dezena, Aluguel

**Card Variação por Componente (só Despesas):**
- Variação de cada componente
- R$ e % de mudança
- Cores por sinal (negativo=vermelho, positivo=verde)

### **Visualização: Por Produto/Rota/Ponto**

**TOP 5 Quedas:**
- Itens com variação negativa
- Cor: Vermelho (valores negativos)
- Card breakdown por item

**TOP 5 Crescimentos:**
- Itens com variação positiva
- Cor: Verde (valores positivos)
- Card breakdown por item

**Tabela Todos os Itens:**
- Lista completa com variação
- Colunas: Item, Período A, Período B, Variação %, Diferença R$
- Cores por sinal matemático

### **Sistema de Cores**

**IMPORTANTE:** Cores seguem **sinal matemático**, não significado:

| Valor | Cor | Bolinha |
|-------|-----|---------|
| Negativo (-5,79%) | 🔴 Vermelho | 🔴 |
| Positivo (+3,2%) | 🟢 Verde | 🟢 |
| Zero (0%) | 🟢 Verde | 🟢 |

**Exemplo:**
```
Despesas: -6,48% 🔴 (vermelho pois negativo)
Vendas: -11,41% 🔴 (vermelho pois negativo)
```

---

## 📊 **ABA 4: EVOLUÇÃO**

### **Objetivo**
Análise temporal com gráfico de evolução e cards de métricas.

### **Seleção de Período**

**De (Início):**
- Ano
- Mês

**Até (Fim):**
- Ano
- Mês

**💡 Filtros dinâmicos:** "Até" mostra apenas meses ≥ "De" quando mesmo ano.

### **Filtros Opcionais**

| Filtro | Descrição |
|--------|-----------|
| **Produto** | TODOS, JB, LE, BG |
| **Rota** | Todas, 2201... |
| **Ponto** | Todos, 220101... |

### **Gráfico Interativo**

**Características:**
- 📈 Linha Vendas (azul/roxo)
- 📉 Linha Despesas (vermelha) - se disponível
- Eixo X: Períodos (jan/2026, fev/2026...)
- Eixo Y: Valores em R$
- Tooltip: Ao passar mouse mostra valores

**Interações:**
- Hover: Mostra valores exatos
- Pode ocultar/mostrar linhas clicando na legenda

### **5 Cards de Métricas**

#### **1. Período Inicial**
- Vendas: Valor inicial
- Despesas: Valor inicial (se disponível)
- Data: Primeiro mês do período

#### **2. Período Final**
- Vendas: Valor final
- Despesas: Valor final (se disponível)
- Data: Último mês do período

#### **3. Variação Total**
- **Vendas:**
  - Diferença R$: `-R$ 57.570,62`
  - Percentual: `(-11,41%)`
  - Status: 🔻 Queda / 📈 Crescimento
  - Cor: Vermelho (negativo) / Verde (positivo)

- **Despesas:**
  - Diferença R$: `-R$ 6.033,46`
  - Percentual: `(-6,48%)`
  - Status: 🔻 Redução / 📈 Aumento
  - Cor: Vermelho (negativo) / Verde (positivo)

#### **4. Pico Máximo**
- Vendas: Maior valor do período + data
- Despesas: Maior valor do período + data

#### **5. Pico Mínimo**
- Vendas: Menor valor do período + data
- Despesas: Menor valor do período + data

### **Disponibilidade de Despesas**

**Se período inclui dados < 2026:**
- Gráfico: Só linha de vendas
- Cards: Só dados de vendas
- Aviso: "💡 Despesas disponíveis a partir de jan/2026"

**Se período todo ≥ 2026:**
- Gráfico: Vendas + Despesas
- Cards: Vendas + Despesas
- Sem avisos

---

## 🎨 **Sistema de Cores Global**

### **Cores por Sinal (Comparativo/Evolução)**

| Sinal | Cor | Uso |
|-------|-----|-----|
| Negativo (-) | 🔴 Vermelho | Valores com `-` |
| Positivo (+) | 🟢 Verde | Valores com `+` |
| Zero (0) | 🟢 Verde | Valores = 0 |

**Importante:** Não há interpretação de "bom" ou "ruim", apenas sinal matemático.

### **Cores por Status (Despesas)**

| Status | Cor | Threshold |
|--------|-----|-----------|
| Ideal | 🟢 Verde | < 25% |
| Atenção | 🟡 Amarelo | 25-35% |
| Crítico | 🔴 Vermelho | > 35% |

---

## 🔧 **Recursos Especiais**

### **1. Filtros Dinâmicos**

**Como funciona:**
- Opções de filtros mudam baseado em seleções anteriores
- Mostra apenas dados disponíveis no contexto

**Exemplo Comparativo:**
```
Seleciona: Período A=jan/2026, Período B=fev/2026
Resultado: Filtro "Rota" mostra apenas rotas em jan OU fev

Seleciona: Rota=2201
Resultado: Filtro "Ponto" mostra apenas pontos da rota 2201
```

### **2. Ocultar Registros Zero**

**Vendas/Despesas:**
- Registros com valor 0 no produto filtrado **não aparecem**

**Exemplo:**
```
Filtro: Produto=JB

Código 220101: JB=R$ 5.000 ✅ Aparece
Código 220102: JB=R$ 0     ❌ Não aparece
```

### **3. Breakdown de Componentes**

**Onde aparece:**
- Aba Despesas: Cards e tabela
- Comparativo Despesas: Card variação + períodos A/B
- Por Produto/Rota/Ponto: Card por item

**O que mostra:**
- 💵 Comissão: Valor e %
- 📦 Dezena: Valor e %
- 🏠 Aluguel: Valor e %

**Regras:**
- Se valor = 0 → não aparece
- Se "Sem Comissão" ativo → comissão não aparece
- Se produto = CN → comissão nunca aparece

### **4. Cálculo de % de Custo**

**Fórmula:**
```
% Custo = (Despesas / Vendas) × 100
```

**Exemplo:**
```
Vendas: R$ 100.000
Despesas: R$ 25.000
% Custo = 25%
```

**Com "Sem Comissão":**
```
Vendas: R$ 100.000
Despesas (sem comissão): R$ 18.000
% Custo = 18%
```

### **5. Formatação de Valores**

**Monetário:**
- Sempre completo: `R$ 15.641.875,81`
- Nunca abreviado: ~~`R$ 15.6M`~~
- Font-size dinâmico para caber

**Percentual:**
- 2 casas decimais: `12,34%`
- Sinal explícito: `+5,67%` ou `-3,21%`

---

## 📱 **Responsividade**

**Desktop (>1024px):**
- Layout multi-colunas
- Cards lado a lado
- Tabelas completas

**Tablet (768-1024px):**
- 2 colunas
- Cards empilhados
- Scroll horizontal em tabelas

**Mobile (<768px):**
- 1 coluna
- Cards empilhados
- Scroll horizontal em tabelas

---

## 🖨️ **Exportação para PDF**

### **Como Funciona**

1. Configure filtros desejados
2. Clique "🖨️ Imprimir / Salvar PDF"
3. Abre janela de impressão nativa
4. Escolha "Salvar como PDF"
5. Ajuste layout (Paisagem recomendado)
6. Salvar

### **O que é Exportado**

**Incluído:**
- ✅ Filtros atuais
- ✅ Cards visíveis
- ✅ Tabelas completas
- ✅ Gráficos (Evolução)

**Não incluído:**
- ❌ Abas não selecionadas
- ❌ Botões interativos

### **Dicas para Melhor PDF**

- Use **Paisagem** para tabelas largas
- Desative "Cabeçalhos e rodapés"
- Use "Ajustar à página"
- Escala: 80-100%

---

## ⚡ **Performance**

### **Otimizações Implementadas**

- ✅ Processamento client-side (sem servidor)
- ✅ Caching de dados em memória
- ✅ Renderização sob demanda
- ✅ Validações com guardas robustas

### **Limites Recomendados**

| Item | Limite | Performance |
|------|--------|-------------|
| Registros | < 10.000 | Excelente |
| Registros | 10.000 - 50.000 | Boa |
| Registros | > 50.000 | Pode demorar |
| Arquivo | < 5MB | Ótima |
| Arquivo | 5-10MB | Boa |
| Arquivo | > 10MB | Lenta |

---

## 🛡️ **Validações e Segurança**

### **Validações Automáticas**

- ✅ State inicializado corretamente
- ✅ Arrays não vazios antes de `.map()`
- ✅ Divisões por zero tratadas
- ✅ Try/catch em operações críticas
- ✅ Fallbacks para dados ausentes

### **Segurança**

- ✅ **100% Client-side**: Dados nunca saem do navegador
- ✅ Sem backend: Sem risco de vazamento
- ✅ Sem upload: Arquivo processado localmente
- ✅ Sem cookies ou tracking

---

**✅ Documentação completa! Para dúvidas específicas, consulte outras seções.**

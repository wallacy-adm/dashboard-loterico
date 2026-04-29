# 🤖 CLAUDE.md - Instruções para Claude Code

> **ATENÇÃO:** Este arquivo é lido automaticamente pelo Claude Code. Contém TODO o contexto necessário para trabalhar neste projeto.

---

## 👤 SOBRE O USUÁRIO

**Nome:** Wallacy

**Características importantes:**
- ❌ **NÃO programa** (nenhuma habilidade técnica)
- ✅ Conhece muito o negócio (vendas e despesas)
- ✅ Direto, objetivo, prefere ação rápida
- ✅ Quer resultados práticos, não teoria
- ✅ Valoriza economia de tokens (preferência por edições cirúrgicas)

**Estilo de comunicação preferido:**
- Português brasileiro
- Direto e claro (sem floreios)
- Estruturado (com seções, listas, emojis)
- Pouco texto, muita ação
- Sempre mostrar status do que foi feito

---

## 📋 SOBRE O PROJETO

**Nome:** Dashboard Gerencial - Análise de Vendas e Despesas

**O que faz:**
Sistema HTML/JavaScript single-page para análise de dados de vendas e despesas a partir de planilhas Excel.

**Versão atual:** 1.1.0

**Stack técnica:**
- HTML5 + JavaScript (puro, sem frameworks)
- Tailwind CSS (via CDN)
- Chart.js (visualizações)
- ExcelJS (leitura de planilhas)
- Processamento 100% client-side (sem backend)

**Arquivo principal:**
- `dashboard.html` - Arquivo único do projeto (editar direto aqui)

---

## 🎯 ESTRUTURA DO DASHBOARD

### **4 Abas Principais:**

1. **Vendas** - Visualização detalhada por produto
2. **Despesas** - Análise de custo percentual
3. **Comparativo** - Comparação entre 2 períodos
4. **Evolução** - Análise temporal multi-período

### **6 Planilhas Excel Processadas:**
- `vendas` - Dados de vendas por produto
- `dezena` - Despesa de dezenas
- `comissao_jb` - Comissões do produto JB
- `comissao_le` - Comissões do produto LE
- `comissao_bg` - Comissões do produto BG
- `aluguel` - Aluguel fixo por código

### **4 Produtos:**
- **JB** - Jogo do Bicho
- **LE** - Loteria
- **BG** - Bingo
- **CN** - Caça-Níquel ⚠️ **NUNCA tem comissão**

---

## 🔑 REGRAS DE NEGÓCIO CRÍTICAS

### **1. Formato de Código:**
```
RRRRPP (6 dígitos)
├── RRRR = Rota (4 dígitos)
└── PP = Ponto (2 dígitos)

Exemplo: 220505
├── 2205 = Rota
└── 05 = Ponto
```

⚠️ **SEMPRE exibir como 6 dígitos completos** (ex: `220505`, NUNCA só `05`)

### **2. CN Nunca Tem Comissão:**
```javascript
// ❌ ERRADO
if (produto === 'cn') aplicarComissao();

// ✅ CORRETO
if (produto !== 'cn') aplicarComissao();
```

### **3. Aluguel Sem Coluna de Data:**
- Aluguel é **fixo por código**
- **Não tem coluna mês/ano**
- Aplica-se a todos os meses

### **4. Chave Única para Despesas:**
```
chave = `${codigo}-${mes}-${ano}`
Exemplo: "220505-jan-2026"
```

### **5. Despesas Disponíveis Apenas a Partir de Jan/2026:**
- Antes de jan/2026: Sem dados de despesas
- Aba Comparativo: Filtra automaticamente períodos < 2026

### **6. Thresholds de Custo Percentual:**
```
< 25%  = 🟢 Verde   (Ideal)
25-35% = 🟡 Amarelo (Atenção)
> 35%  = 🔴 Vermelho (Crítico)
```

### **7. Cores por Sinal Matemático:**
```
Negativo (-)  = 🔴 Vermelho
Positivo (+)  = 🟢 Verde
Zero (0)      = ⚪ Cinza
```
**NÃO usar semântica de negócio** (ex: "menos despesa é bom = verde")

### **8. Meses em Ordem CRONOLÓGICA:**
```javascript
// ✅ CORRETO
['jan', 'fev', 'mar', 'abr', 'mai', 'jun', 'jul', 'ago', 'set', 'out', 'nov', 'dez']

// ❌ ERRADO (alfabético)
['abr', 'ago', 'dez', 'fev', 'jan', 'jul', 'jun', 'mai', 'mar', 'nov', 'out', 'set']
```

---

## 💻 PADRÕES DE CÓDIGO

### **🚨 REGRA #1: EDIÇÕES CIRÚRGICAS**

**SEMPRE faça:**
- Use `grep` para localizar linha exata
- Use `view` para ver contexto (~60 linhas)
- Use `str_replace` com contexto suficiente

**NUNCA faça:**
- ❌ Reescrever o arquivo inteiro
- ❌ Refatorar sem necessidade
- ❌ Mudar estrutura sem aviso prévio
- ❌ Quebrar funcionalidades existentes

### **Workflow Padrão de Edição:**

```bash
# 1. Localizar função
grep -n "function nomeDaFuncao" dashboard.html

# 2. Ver contexto (linha encontrada ± 30)
view dashboard.html [linha-30, linha+30]

# 3. Editar cirurgicamente
str_replace com contexto suficiente

# 4. Atualizar CHANGELOG.md (sempre!)
```

### **Estrutura do Código:**

```
dashboard.html
├── Linha 1-100:    HTML base + Tailwind + CDNs
├── Linha 100-200:  State e configurações iniciais
├── Linha 200-700:  Processamento de dados (Excel)
├── Linha 700-900:  Filtros e helpers
├── Linha 900-1500: Renderização Aba Vendas
├── Linha 1500-2000: Renderização Aba Despesas
├── Linha 2000-2200: Renderização Aba Comparativo
├── Linha 2200-2900: Renderização Aba Evolução
└── Linha 2900-3000: Inicialização e eventos
```

⚠️ **Linhas são aproximadas** - sempre use `grep` para localização exata.

---

## 📊 FUNÇÕES PRINCIPAIS (Mapa Mental)

### **Processamento:**
- `processarPlanilha()` - Lê arquivo Excel
- `processarVendas()` - Processa dados de vendas
- `processarDespesas()` - Processa comissão/dezena/aluguel

### **Filtros:**
- `getOpcoesEvolucao()` - Filtros dinâmicos da Evolução
- `aplicarFiltros()` - Aplica filtros aos dados
- `calcularPontosPorPeriodo()` - Agrupa vendas por ponto/período

### **Renderização:**
- `renderVendas()` - Aba Vendas
- `renderDespesas()` - Aba Despesas
- `renderComparativo()` - Aba Comparativo
- `renderEvolucao()` - Aba Evolução
- `renderResultadoEvolucao()` - Resultado da Evolução

### **Gráficos (Chart.js):**
- `criarGraficoEvolucao()` - Gráfico misto (barras + linha)
- `criarGraficoComparativo()` - Gráfico de barras
- `criarGraficoVendas()` - Distribuição por produto
- `toggleDataset()` - Toggle individual de datasets

### **Helpers:**
- `fmt(valor)` - Formata valores monetários
- `log(...args)` - Log condicional (DEBUG = false)

---

## 🎨 PADRÃO VISUAL

### **Cores Primárias:**
```css
--primary:        #8b5cf6 (Roxo)
--success:        #10b981 (Verde)
--warning:        #f59e0b (Amarelo)
--danger:         #dc2626 (Vermelho)
--info:           #3b82f6 (Azul)
```

### **Cores do Gráfico Misto (Evolução):**
```javascript
const coresPontos = [
    { border: '#10b981', bg: 'rgba(16, 185, 129, 0.8)' },  // Verde
    { border: '#3b82f6', bg: 'rgba(59, 130, 246, 0.8)' },  // Azul
    { border: '#f59e0b', bg: 'rgba(245, 158, 11, 0.8)' },  // Amarelo
    { border: '#ef4444', bg: 'rgba(239, 68, 68, 0.8)' },   // Vermelho
    { border: '#8b5cf6', bg: 'rgba(139, 92, 246, 0.8)' },  // Roxo
    { border: '#06b6d4', bg: 'rgba(6, 182, 212, 0.8)' },   // Cyan
    { border: '#84cc16', bg: 'rgba(132, 204, 22, 0.8)' },  // Lima
    { border: '#f97316', bg: 'rgba(249, 115, 22, 0.8)' },  // Laranja
    { border: '#ec4899', bg: 'rgba(236, 72, 153, 0.8)' },  // Rosa
    { border: '#6b7280', bg: 'rgba(107, 114, 128, 0.8)' }  // Cinza
];

// Linha TOTAL
const corTotal = '#7c3aed'; // Roxo escuro tracejado
```

### **Layout:**
- Cards: `bg-white rounded-lg shadow-md p-4`
- Cards stack vertical: `space-y-3` (NÃO usar grid)
- Spacing consistente: `gap-4` ou `gap-6`

---

## 📝 HISTÓRICO DE DECISÕES

### **Por que Chart.js?**
- ✅ Leve e fácil de usar
- ✅ Suporta gráficos mistos nativamente
- ✅ Boa documentação
- ✅ CDN disponível

### **Por que Gráfico Misto na Evolução?**
**Histórico:**
1. Tentou-se múltiplas linhas → confuso (sobreposição)
2. Avaliou-se barras agrupadas → bom mas sem total
3. **Avaliou-se heatmap → bom mas requer "educação"**
4. ✅ **ESCOLHIDO: Misto (barras + linha total)**
   - Detalhe de cada ponto (barras)
   - Visão macro (linha tracejada total)
   - Zero confusão visual
   - Profissional sem complexidade

### **Por que Top 10 Pontos?**
- Performance (renderização rápida)
- Clareza visual (mais que 10 polui)
- Cobre 90%+ dos casos de análise

### **Por que Cards Vertical (space-y-3)?**
- Melhor responsividade mobile
- Leitura sequencial mais clara
- Wallacy preferiu visualmente

### **Por que Filtro Dinâmico de Pontos?**
**Problema:** Dropdown mostrava TODOS pontos, mesmo sem vendas do produto.
**Solução:** Filtrar pontos com vendas > 0 do produto selecionado.
**Impacto:** Análise mais focada, menos cliques perdidos.

---

## 🔧 WORKFLOW DE TAREFAS COMUNS

### **Tarefa: Corrigir Bug**
```
1. Reproduzir o bug (entender)
2. grep para localizar código relevante no dashboard.html
3. view contexto completo (~60 linhas)
4. str_replace cirúrgico
5. Atualizar CHANGELOG.md
6. Testar mentalmente
```

### **Tarefa: Adicionar Feature**
```
1. Entender requisito (perguntar se necessário)
2. Mostrar mockup visual ANTES (visualize:show_widget)
3. Implementar cirurgicamente no dashboard.html
4. Atualizar CHANGELOG.md (incrementar versão)
5. Atualizar este CLAUDE.md se necessário
```

### **Tarefa: Modificar Visual**
```
1. SEMPRE mostrar preview ANTES (visualize:show_widget)
2. Usar cores hardcoded (hex), não CSS variables
3. Implementar no dashboard.html
```

### **Tarefa: Refatoração**
```
⚠️ NUNCA refatorar sem solicitação explícita
Se Wallacy pedir:
1. Explicar o que vai mudar
2. Mostrar antes/depois
3. Aguardar aprovação
4. Fazer em pequenos passos
```

---

## ⚠️ ARMADILHAS COMUNS

### **1. Tokens limitados em artefatos**
- Limite ~15k caracteres por artefato React
- Por isso o projeto migrou para HTML único
- **NÃO tentar criar artefatos React separados**

### **2. Cores baseadas em sinal**
```javascript
// ❌ ERRADO
const cor = variacaoVendas > 0 ? 'verde' : 'vermelho'; // (semântica de negócio)

// ✅ CORRETO
const cor = valor < 0 ? 'vermelho' : valor > 0 ? 'verde' : 'cinza'; // (sinal matemático)
```

### **3. Filtros desincronizados**
- Filtro de produto deve afetar **tabelas E cards** simultaneamente
- Registros com 0 vendas do produto selecionado devem ser **ocultados**

### **4. CN com comissão**
- **JAMAIS** mostrar comissão para CN
- Sempre validar: `if (produto !== 'cn')`

### **5. Cards de Status**
- **DEVEM** corresponder às tabelas exatamente
- Ideal/Atenção/Crítico calculados igual em todos os lugares

---

## 🎯 INSTRUÇÕES FINAIS PARA CLAUDE CODE

Quando o Wallacy pedir algo:

1. **Leia este CLAUDE.md primeiro** (você já fez isso!)
2. **Leia o CHANGELOG.md** para ver histórico recente
3. **Confirme entendimento** antes de executar (se complexo)
4. **Mostre preview visual** se for mudança de UI
5. **Faça edições cirúrgicas em `dashboard.html`** (nunca reescreva tudo)
6. **Atualize documentação** (CHANGELOG.md sempre)
7. **Reporte status claro** ao final

### **Comunicação com Wallacy:**
- Português BR
- Direto e estruturado
- Use emojis para hierarquia visual
- Mostre status (✅ ❌ ⏳ 🔄)
- Seja proativo em sugerir melhorias
- **Critique construtivamente** (Wallacy quer feedback honesto)

---

## 📚 DOCUMENTAÇÃO ADICIONAL

Para mais detalhes, consulte:

- `README.md` - Visão geral do projeto
- `CHANGELOG.md` - Histórico de versões
- `docs/DEVELOPMENT.md` - Guia de desenvolvimento
- `docs/BUSINESS-RULES.md` - Regras de negócio detalhadas
- `docs/DATA-STRUCTURE.md` - Estrutura das planilhas
- `docs/CONTEXT.md` - Contexto histórico do projeto
- `docs/FUNCIONALIDADES.md` - Funcionalidades detalhadas
- `docs/INSTALACAO.md` - Instruções de instalação/uso
- `docs/COMO-PUBLICAR.md` - Como publicar atualizações
- `docs/PROMPTS-CLAUDE-CODE.md` - Templates de prompts úteis

---

**Última atualização:** 2026-04-29 (v1.2.0)

**Mantenedor:** Wallacy + Claude (Anthropic)

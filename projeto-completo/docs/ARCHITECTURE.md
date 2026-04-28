# 🏗️ ARQUITETURA - Decisões Técnicas

> Documento explicando as principais decisões arquiteturais do projeto e o "porquê" de cada escolha.

---

## 🎯 Visão Geral

**Tipo de Aplicação:** Single-Page Application (SPA)
**Arquitetura:** Client-Side (100% no navegador)
**Padrão:** State-driven rendering (re-renderização baseada em mudanças de estado)

---

## 🧩 Por que Single HTML File?

### Histórico
1. **Início:** Múltiplos artefatos React separados
2. **Problema:** Limite de ~15k caracteres por artefato (Claude.ai)
3. **Solução:** Migrar para HTML único com JavaScript inline

### Benefícios
- ✅ **Portabilidade total** - Um arquivo, copia e usa
- ✅ **Sem build** - Sem webpack, npm, dependências
- ✅ **Funciona offline** após primeiro carregamento
- ✅ **Fácil distribuir** - email, pendrive, GitHub
- ✅ **Wallacy pode usar** sem conhecimento técnico

### Trade-offs
- ⚠️ Arquivo grande (~3.000+ linhas)
- ⚠️ Sem hot reload em desenvolvimento
- ⚠️ Mais difícil de testar unitariamente

**Veredicto:** Trade-off vale a pena. Simplicidade > complexidade.

---

## 📦 Por que Sem Frameworks?

### Considerados:
- **React** ❌ - Requer build, complexidade desnecessária
- **Vue** ❌ - Mesma situação do React
- **Alpine.js** 🤔 - Considerado, mas vanilla JS já é suficiente
- **Vanilla JS** ✅ - **ESCOLHIDO**

### Justificativa
- Wallacy não programa
- Manutenção precisa ser simples
- Vanilla JS + Tailwind = poderoso e simples
- Performance nativa (sem overhead)

---

## 📊 Por que Chart.js?

### Bibliotecas avaliadas:
| Biblioteca   | Prós                          | Contras                    |
|--------------|-------------------------------|----------------------------|
| Chart.js     | Leve, simples, gráficos mistos| -                          |
| D3.js        | Poderoso, customizável        | Curva de aprendizado alta  |
| ApexCharts   | Bonito, animações             | Mais pesado                |
| Plotly       | Cientifico, completo          | Pesado demais              |
| Recharts     | React-native                  | Requer React               |

### Decisão: Chart.js
- ✅ CDN disponível (sem npm)
- ✅ Suporta gráficos mistos nativamente
- ✅ Documentação excelente
- ✅ ~60kb (leve)
- ✅ API simples

---

## 🎨 Por que Tailwind CSS?

### Alternativas consideradas:
- **Bootstrap** ❌ - Componentes pré-prontos limitam customização
- **CSS puro** ❌ - Verboso demais para projeto deste tamanho
- **Tailwind** ✅ - Utility-first, rápido, customizável

### Configuração
- Via CDN (sem build)
- Sem arquivo `tailwind.config.js`
- Apenas classes core (sem plugins)

---

## 📁 Estrutura de Dados

### State Centralizado

```javascript
const state = {
    dados: {
        vendas: [],       // Array de objetos
        dezena: [],
        comissao: { jb: [], le: [], bg: [] },
        aluguel: []
    },
    filtros: {
        vendas: { ... },
        despesas: { ... },
        comparativo: { ... },
        evolucao: { ... }
    },
    charts: { ... },     // Instâncias Chart.js
    cache: { ... }       // Cache para performance
};
```

**Padrão:** Single source of truth. Modificações no state disparam re-renderização.

### Por que não Redux/Zustand?
- Complexidade desnecessária
- Object plain JS é suficiente
- Sem necessidade de dev tools

---

## 🔄 Padrão de Renderização

### State → Render

```
1. Usuário muda filtro
   ↓
2. state.filtros.X = novoValor
   ↓
3. render() é chamado
   ↓
4. renderTabAtiva() processa state
   ↓
5. DOM é atualizado
   ↓
6. Charts são recriados (se necessário)
```

### Funções de Render (uma por aba)
- `renderVendas()` - Aba Vendas
- `renderDespesas()` - Aba Despesas
- `renderComparativo()` - Aba Comparativo
- `renderEvolucao()` - Aba Evolução

### Princípio
**Não manipular DOM diretamente fora das funções render.** Sempre via state.

---

## 📈 Por que Gráfico Misto na Evolução?

### Histórico de Iterações

#### v1.0.0 - Linha simples agregada
- 1 linha roxa para toda a rota
- ✅ Simples
- ❌ Não mostra detalhe por ponto

#### v1.1.0-beta1 - Múltiplas linhas
- 1 linha por ponto (até 10)
- ❌ **Confuso!** Linhas se sobrepõem
- ❌ Difícil distinguir cores

#### v1.1.0-beta2 - Avaliações alternativas
- **Barras agrupadas:** Bom, mas sem total
- **Heatmap:** Bom, mas requer "educação"
- **Misto (barras + linha):** ✅ **ESCOLHIDO!**

#### v1.1.0 - FINAL - Gráfico Misto
- ✅ Barras coloridas (cada ponto)
- ✅ Linha tracejada roxa (total geral)
- ✅ Detalhe + visão macro
- ✅ Zero confusão visual

### Por que essa combinação venceu?
1. **Detalhe:** Barras mostram cada ponto individualmente
2. **Macro:** Linha mostra o total geral como referência
3. **Comparação:** Fácil comparar ponto vs total
4. **Familiar:** Todo mundo entende barras + linha
5. **Profissional:** Padrão em dashboards corporativos

---

## 🎨 Sistema de Cores

### Cores por Sinal Matemático

```javascript
// REGRA: Cor segue o sinal, NÃO a semântica de negócio
const corVariacao = (valor) => {
    if (valor < 0) return 'vermelho';  // Negativo = vermelho SEMPRE
    if (valor > 0) return 'verde';     // Positivo = verde SEMPRE
    return 'cinza';                     // Zero = cinza
};
```

**Por quê?**
- Consistência visual
- Não causa confusão (ex: "menos despesa é bom = verde" pode confundir)
- Padrão financeiro internacional

### Cores de Status (Custo Percentual)

```javascript
// Thresholds fixos
const statusCusto = (percentual) => {
    if (percentual < 25)  return { cor: 'verde',    label: 'Ideal' };
    if (percentual <= 35) return { cor: 'amarelo',  label: 'Atenção' };
    return                       { cor: 'vermelho', label: 'Crítico' };
};
```

**Por que esses valores?**
- Definidos pelo Wallacy baseado em experiência de negócio
- Refletem realidade do mercado de jogos populares
- Fácil ajustar se necessário (1 lugar no código)

---

## ⚡ Otimizações de Performance

### 1. Cache de Cálculos
```javascript
state.cache = {
    vendas_total: null,
    despesas_total: null,
    // Limpa quando dados mudam
};
```

### 2. Limite de Pontos no Gráfico
- **Top 10 pontos** apenas
- Evita poluição visual
- Mantém renderização rápida

### 3. Debounce em Filtros
- Evita re-renders excessivos
- Aplica filtro após 100ms de inatividade

### 4. Lazy Loading de Charts
- Charts criados apenas quando aba é ativa
- Destruídos ao mudar de aba

---

## 🔒 Validações (GUARDA Pattern)

```javascript
function processarVendas(planilha) {
    // GUARD 1: Planilha existe?
    if (!planilha) return [];
    
    // GUARD 2: Tem cabeçalho?
    if (planilha.length < 2) return [];
    
    // GUARD 3: Colunas obrigatórias?
    const cols = planilha[0];
    if (!cols.includes('codigo')) {
        log('❌ Coluna "codigo" não encontrada');
        return [];
    }
    
    // PROCESSAMENTO (só executa se passar nos guards)
    return planilha.slice(1).map(...);
}
```

**Por quê?**
- Falhas silenciosas e graceful
- Não quebra a UI com dados ruins
- Logs para debug (DEBUG = false em produção)

---

## 🎯 Princípios de Design

### 1. **KISS (Keep It Simple, Stupid)**
- Sem abstrações desnecessárias
- Código direto e legível
- Wallacy precisa entender o que faz

### 2. **DRY (Don't Repeat Yourself) - com moderação**
- Helpers reutilizáveis (`fmt`, `log`)
- Mas não over-engineer
- Duplicação leve > abstração complexa

### 3. **YAGNI (You Aren't Gonna Need It)**
- Não implementar features "para o futuro"
- Adicionar quando necessário
- Manter código enxuto

### 4. **Convention over Configuration**
- Nomes de planilhas fixos
- Estrutura de dados padronizada
- Filtros têm comportamento previsível

---

## 🔮 Decisões Adiadas (Não Implementadas)

### 1. Backend / API
- **Decisão:** Não implementar
- **Razão:** Wallacy não tem servidor, não quer manter

### 2. Banco de dados
- **Decisão:** Não implementar
- **Razão:** Excel é a fonte de verdade, dashboard é leitor

### 3. Autenticação
- **Decisão:** Não implementar
- **Razão:** Uso pessoal/equipe pequena, dados sensíveis ficam no PC

### 4. Multi-idioma
- **Decisão:** Apenas Português BR
- **Razão:** Wallacy só usa em português

### 5. Mobile-first
- **Decisão:** Desktop-first com responsividade
- **Razão:** Análise de dados em desktop é melhor experiência

---

## 📚 Referências

- [Chart.js Docs](https://www.chartjs.org/docs/latest/)
- [Tailwind CSS Docs](https://tailwindcss.com/docs)
- [ExcelJS Docs](https://github.com/exceljs/exceljs)
- [MDN Web Docs](https://developer.mozilla.org/)

---

**Última atualização:** 2026-04-28 (v1.1.0)

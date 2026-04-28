# Changelog

Todas as mudanças notáveis neste projeto serão documentadas neste arquivo.

O formato é baseado em [Keep a Changelog](https://keepachangelog.com/pt-BR/1.0.0/),
e este projeto adere ao [Semantic Versioning](https://semver.org/lang/pt-BR/).

---

## [1.1.0] - 2026-03-31

### ✨ Adicionado
- **Filtro Dinâmico de Pontos**: Dropdown "Ponto" agora mostra apenas pontos com vendas > 0 do produto selecionado, eliminando pontos irrelevantes e focando a análise
- **Toggle "Mostrar Todos os Pontos"**: Nova opção na aba Evolução que permite visualizar dados de múltiplos pontos simultaneamente
- **Gráfico Misto (Barras + Linha)**: Quando o toggle está ativado, o gráfico exibe:
  - Barras coloridas para cada ponto individual (top 10 por vendas)
  - Linha roxa tracejada representando o TOTAL geral
  - Paleta de 10 cores distintas para fácil identificação
  - Legenda customizada à esquerda com interatividade (click para toggle)

### 🔧 Melhorado
- **UX da Aba Evolução**: Interface mais intuitiva com indicadores visuais claros do estado do toggle
- **Performance**: Otimização no cálculo de dados por ponto e período
- **Legenda Interativa**: Click nos itens da legenda permite mostrar/ocultar datasets individuais
- **Layout Responsivo**: Gráfico com legenda à esquerda (110px fixo) + área do gráfico flexível

### 📊 Detalhes Técnicos
- Função `calcularPontosPorPeriodo()` para agrupar vendas por ponto e período
- Suporte a gráficos mistos (mixed charts) no Chart.js
- Limitação automática a top 10 pontos para evitar poluição visual
- Cores com gradientes e opacity 0.8 para melhor contraste

---

## [1.0.0] - 2026-03-30

### ✨ Lançamento Inicial
- Dashboard gerencial HTML/JavaScript completo para análise de vendas e despesas
- Processamento de 6 planilhas Excel: vendas, dezena, comissao_jb, comissao_le, comissao_bg, aluguel
- 4 abas principais: Vendas, Despesas, Comparativo, Evolução

### 📊 Funcionalidades Principais

#### Aba Vendas
- Visualização detalhada de vendas por produto (JB, LE, BG, CN)
- Filtros por ano, mês, rota e ponto
- Cards com métricas principais (total, ticket médio, pontos ativos)
- Tabela detalhada com breakdown por produto
- Gráfico de distribuição por produto

#### Aba Despesas
- Análise de custo percentual (Vendas vs Despesas)
- Três componentes: Comissão, Dezena, Aluguel
- Sistema de alertas por faixa (ideal <25%, atenção 25-35%, crítico >35%)
- Filtros sincronizados com aba Vendas
- Tabela com breakdown detalhado por componente

#### Aba Comparativo
- Comparação entre dois períodos (Período A vs Período B)
- Cards de variação total e por componente
- Análise de crescimento/redução percentual e absoluta
- Suporte apenas para períodos >= 2026 (dados de despesas disponíveis)
- Gráfico de barras comparativo

#### Aba Evolução
- Análise temporal de vendas ao longo de múltiplos meses
- Seleção de período com range (De → Até)
- Gráfico de linha mostrando tendência
- Cards com métricas: período inicial/final, variação %, picos máximo/mínimo
- Opção de visualizar linha de despesas (quando disponível)

### 🔧 Características Técnicas
- Single-page application (SPA) em HTML/JavaScript puro
- Chart.js para visualizações
- ExcelJS para leitura de planilhas
- Processamento client-side (sem backend)
- Sistema de cache para performance
- Validações robustas (GUARDA pattern)

### 🎨 Design
- Interface responsiva com Tailwind CSS
- Tema roxo (#8b5cf6) como cor primária
- Sistema de cores semântico (verde=positivo, vermelho=negativo)
- Cards informativos com ícones
- Feedback visual claro (loading, erros, avisos)

### 📋 Regras de Negócio
- Formato de código: RRRRPP (4 dígitos rota + 2 dígitos ponto)
- Produto CN (Caça-Níquel) nunca tem comissão
- Despesas disponíveis apenas a partir de jan/2026
- Aluguel suporta formato híbrido (com/sem coluna de data)
- Chave única para despesas: `codigo-mes-ano`

### 🐛 Correções Importantes
- **Bug Comparativo**: Período < 2026 não trava mais a interface - filtros permanecem visíveis
- **Cores por Sinal Matemático**: Negativo = vermelho, positivo = verde (não semântica de negócio)
- **Card Variação Total**: Mostra sinal "-" em vendas negativas com cores corretas
- **Cards Período A/B**: Incluem breakdown por componente (Comissão, Dezena, Aluguel)
- **Layout Comparativo**: "Variação por Componente" reposicionado entre cards de período

### 📚 Documentação
- README.md completo com visão geral
- INSTALACAO.md com guia passo a passo
- ESTRUTURA-DADOS.md com formato das planilhas
- FUNCIONALIDADES.md com detalhes de cada aba
- exemplos/README.md com estrutura dos arquivos de exemplo
- LICENSE (MIT)
- .gitignore configurado
- COMO-PUBLICAR-GITHUB.md com instruções de publicação

---

## Legenda de Tipos de Mudança

- **✨ Adicionado**: para novas funcionalidades
- **🔧 Melhorado**: para mudanças em funcionalidades existentes
- **🐛 Corrigido**: para correção de bugs
- **🗑️ Removido**: para funcionalidades removidas
- **⚠️ Descontinuado**: para funcionalidades que serão removidas
- **🔒 Segurança**: para correções de vulnerabilidades
- **📚 Documentação**: para mudanças na documentação
- **📊 Detalhes Técnicos**: para mudanças técnicas internas

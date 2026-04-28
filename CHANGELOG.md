# 📝 Changelog

Todas as mudanças notáveis neste projeto serão documentadas neste arquivo.

O formato é baseado em [Keep a Changelog](https://keepachangelog.com/pt-BR/1.0.0/),
e este projeto adere ao [Versionamento Semântico](https://semver.org/lang/pt-BR/).

---

## [1.0.0] - 2026-03-24

### 🎉 Lançamento Inicial

Primeira versão estável do Dashboard Gerencial.

### ✨ Adicionado

**Estrutura Geral:**
- 4 abas principais: Vendas, Despesas, Comparativo, Evolução
- Processamento de arquivo Excel (.xlsx) com 6 planilhas
- Interface responsiva (desktop, tablet, mobile)
- Sistema de cores inteligente

**Aba Vendas:**
- Análise de faturamento por produto/rota/ponto
- 4 visualizações: Geral, Por Produto, Por Rota, Por Ponto
- Filtros dinâmicos (ano, mês, produto, rota, ponto)
- Cards de métricas principais
- Tabela detalhada com ordenação
- Ranking de melhores performances (🥇🥈🥉)

**Aba Despesas:**
- Breakdown de custos: Comissão + Dezena + Aluguel
- Toggle "Excluir Comissões" para análise sem comissão
- Cálculo automático de % de custo sobre vendas
- Sistema de thresholds: Ideal (<25%), Atenção (25-35%), Crítico (>35%)
- Cards de status com contadores
- TOP 5 Melhor Custo e TOP 5 Maior Despesa
- Tabela com cores por status de custo
- Breakdown detalhado em cards e tabela

**Aba Comparativo:**
- Comparação entre dois períodos (A vs B)
- Toggle Vendas / Despesas
- Validação: Despesas apenas para períodos ≥ 2026
- 4 tipos: Geral, Por Produto, Por Rota, Por Ponto
- Card principal com variação % e status
- Card "Variação por Componente" (breakdown de despesas)
- Cards Período A e B com breakdown
- TOP 5 Quedas e TOP 5 Crescimentos
- Tabela completa com cores por sinal matemático
- Filtros dinâmicos contextuais

**Aba Evolução:**
- Análise temporal com período De → Até
- Gráfico interativo (Chart.js)
- Linhas de Vendas e Despesas
- 5 cards de métricas: Inicial, Final, Variação Total, Pico Máximo, Pico Mínimo
- Filtros opcionais: Produto, Rota, Ponto
- Suporte para períodos com/sem despesas

**Funcionalidades Especiais:**
- Filtros dinâmicos por contexto
- Ocultar registros com valor zero
- Breakdown de componentes de despesas
- Cálculo automático de % de custo
- Sistema de cores por sinal (negativo=vermelho, positivo=verde)
- Formatação monetária completa (sem abreviação)
- Ordem cronológica de meses

**Regras de Negócio:**
- Produtos: JB, LE, BG, CN
- CN nunca tem comissão
- Código formato: RRRRPP (4 dígitos rota + 2 dígitos ponto)
- Aluguel: custo fixo, formato híbrido (com/sem data)
- Thresholds de custo configurados

**Exportação:**
- PDF via impressão nativa (window.print)
- Suporte a html2canvas (download secundário)
- Lazy loading para performance

**Validações e Segurança:**
- Validação de state e dados antes de processar
- Try/catch em operações críticas
- Guardas robustas para evitar erros
- Fallbacks para dados ausentes
- 100% client-side (sem backend)

### 🐛 Corrigido

**Bug Crítico - Travamento ao Selecionar Período <2026:**
- **Problema:** Dashboard travava completamente ao selecionar período anterior a 2026 em modo Despesas
- **Causa:** Validação mostrava aviso mas continuava executando código, causando erro fatal
- **Solução:** Renderização de filtros mesmo quando mostra aviso, permitindo usuário voltar para 2026
- **Impacto:** Sistema blindado contra travamentos

**Bug - Rota 2201 no Comparativo:**
- **Problema:** Filtro de rota sempre resetava para 2201 mesmo selecionando "Todas"
- **Causa:** Linha de código sobrescrevia state com `rotas[0]` após inicialização
- **Solução:** Remoção da linha que sobrescrevia, mantendo state inicial `rota: 'todas'`

**Ajustes Visuais - Cores Inconsistentes:**
- **Problema:** Algumas telas usavam cores por significado, outras por sinal
- **Solução:** Padronização: cores por sinal matemático (negativo=vermelho, positivo=verde)
- **Aplicado em:** Comparativo (tabelas, cards), Evolução (Card Variação Total)

**Ajustes Visuais - Card Variação Total:**
- **Problema:** Faltava sinal "-" em valores negativos de vendas
- **Solução:** Adicionado sinal explícito e cores corretas

**Ajustes Visuais - Breakdown Cards Período A e B:**
- **Problema:** Faltavam nomes dos componentes ("Comissão:", "Dezena:", "Aluguel:")
- **Solução:** Adicionados labels descritivos

**Ajustes Layout - Reposicionamento Card Variação:**
- **Problema:** Card "Variação por Componente" ficava ao lado do card principal
- **Solução:** Reorganização: Card principal sozinho no topo, Variação no meio entre períodos A e B

### 🔒 Segurança

- Processamento 100% client-side
- Nenhum dado enviado para servidor
- Sem cookies ou tracking
- Sem dependências com vulnerabilidades conhecidas

### 📚 Documentação

- README.md completo com quick start
- INSTALACAO.md com guia passo a passo
- ESTRUTURA-DADOS.md detalhando formato Excel
- FUNCIONALIDADES.md com todas as features
- CHANGELOG.md (este arquivo)
- Template Excel de exemplo

### 🎨 Estilo

- Tailwind CSS via CDN
- Sistema de cores consistente
- Interface responsiva
- Cards com bordas e cores temáticas
- Emojis para indicadores visuais
- Font-size dinâmico para valores monetários

### ⚡ Performance

- Lazy loading de bibliotecas PDF
- Caching de dados em memória
- Renderização sob demanda
- Validações otimizadas

---

## [Não Lançado] - Planejado

### 🔮 Recursos Futuros Considerados

- [ ] Modo escuro (dark mode)
- [ ] Exportação para Excel
- [ ] Mais opções de gráficos
- [ ] Filtros salvos (favoritos)
- [ ] Comparação de múltiplos períodos (A vs B vs C)
- [ ] Dashboard personalizável (drag and drop)
- [ ] Alertas automáticos (email/notificação)
- [ ] Histórico de arquivos carregados
- [ ] Anotações em períodos específicos
- [ ] Metas e objetivos configuráveis

---

## Tipos de Mudanças

- **Adicionado** para novas funcionalidades
- **Modificado** para mudanças em funcionalidades existentes
- **Depreciado** para funcionalidades que serão removidas
- **Removido** para funcionalidades removidas
- **Corrigido** para correção de bugs
- **Segurança** para vulnerabilidades

---

## Como Atualizar Este Arquivo

Ao fazer mudanças no projeto:

1. Adicione entrada na seção `[Não Lançado]`
2. Use o tipo correto (Adicionado, Modificado, etc.)
3. Seja descritivo mas conciso
4. Inclua contexto quando necessário
5. Ao lançar nova versão, mova de "Não Lançado" para nova versão com data

**Exemplo:**
```markdown
## [Não Lançado]

### Adicionado
- Novo filtro de intervalo de datas no Comparativo

### Corrigido
- Bug onde aluguel não aparecia em alguns pontos
```

---

**Versão Atual:** 1.0.0  
**Data do Último Update:** 2026-03-24

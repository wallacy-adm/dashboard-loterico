# 📊 Dashboard Gerencial - Análise de Vendas e Despesas

> Sistema completo para análise de vendas e despesas a partir de planilhas Excel, com visualizações interativas e filtros dinâmicos.

[![Versão](https://img.shields.io/badge/versão-1.1.0-blue.svg)](CHANGELOG.md)
[![Licença](https://img.shields.io/badge/licença-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-ativo-success.svg)]()

---

## 🎯 O que é?

Um dashboard gerencial completo, construído em HTML/JavaScript puro, que processa planilhas Excel localmente (sem servidor) e gera análises visuais profissionais para tomada de decisão em negócios de vendas com múltiplos produtos.

### Principais Funcionalidades

- ✅ **Análise de Vendas** por produto e ponto de venda
- ✅ **Análise de Despesas** com cálculo automático de custo percentual
- ✅ **Comparativo** entre dois períodos
- ✅ **Evolução Temporal** com gráficos mistos (barras + linha)
- ✅ **Filtros Dinâmicos** que se adaptam aos dados disponíveis
- ✅ **Sistema de Alertas** visuais (verde/amarelo/vermelho)
- ✅ **100% Client-Side** - sem servidor, sem instalação

---

## 🚀 Início Rápido

1. **Baixe o arquivo** `dashboard.html`
2. **Abra no navegador** (Chrome, Firefox, Edge)
3. **Faça upload** das suas planilhas Excel
4. **Pronto!** Análise automática

📖 **Guia detalhado:** [docs/INSTALACAO.md](docs/INSTALACAO.md)

---

## 📋 Estrutura do Projeto

```
projeto/
├── 📄 dashboard.html                    # 🎯 ARQUIVO PRINCIPAL (use este!)
├── 📄 dashboard-COMPLETO-OTIMIZADO.html # Cópia de trabalho (idêntica)
├── 📄 README.md                         # Este arquivo
├── 📄 CLAUDE.md                         # 🤖 Instruções para Claude Code
├── 📄 CHANGELOG.md                      # Histórico de versões
├── 📄 LICENSE                           # Licença MIT
│
├── 📁 docs/                             # Documentação detalhada
│   ├── ARCHITECTURE.md                  # Decisões técnicas
│   ├── DEVELOPMENT.md                   # Guia de desenvolvimento
│   ├── BUSINESS-RULES.md                # Regras de negócio
│   ├── DATA-STRUCTURE.md                # Estrutura das planilhas
│   ├── CONTEXT.md                       # Contexto histórico
│   ├── INSTALACAO.md                    # Como instalar/usar
│   ├── FUNCIONALIDADES.md               # Detalhes das abas
│   └── PROMPTS-CLAUDE-CODE.md           # Templates de prompts
│
└── 📁 exemplos/                         # Planilhas de exemplo
    └── README.md                        # Estrutura dos exemplos
```

---

## 📊 As 4 Abas do Dashboard

### 1. 💰 Vendas
- Visualização detalhada por produto (JB, LE, BG, CN)
- Cards com métricas: total, ticket médio, pontos ativos
- Tabela com breakdown por código
- Gráfico de distribuição por produto

### 2. 💸 Despesas
- Análise de custo percentual (Vendas vs Despesas)
- Componentes: Comissão, Dezena, Aluguel
- Sistema de alertas: 🟢 < 25% | 🟡 25-35% | 🔴 > 35%
- Filtros sincronizados com Vendas

### 3. ⚖️ Comparativo
- Compara dois períodos (A vs B)
- Cards de variação total e por componente
- Análise de crescimento/redução
- Gráfico de barras comparativo

### 4. 📈 Evolução
- Análise temporal multi-período
- **Gráfico Misto:** Barras coloridas (cada ponto) + Linha tracejada (total geral)
- Cards: período inicial/final, variação %, picos
- Toggle para mostrar todos os pontos individualmente

---

## 🎯 Produtos Suportados

| Código | Produto       | Comissão? |
|--------|---------------|-----------|
| **JB** | Jogo do Bicho | ✅ Sim    |
| **LE** | Loteria       | ✅ Sim    |
| **BG** | Bingo         | ✅ Sim    |
| **CN** | Caça-Níquel   | ❌ Nunca  |

---

## 🔧 Stack Técnica

- **HTML5 + JavaScript** - Sem frameworks, código simples
- **Tailwind CSS** - Estilização via CDN
- **Chart.js** - Visualizações (linhas, barras, mistos)
- **ExcelJS** - Leitura de arquivos .xlsx
- **100% Client-Side** - Privacidade total, sem upload de dados

---

## 🤖 Para Desenvolvedores e Claude Code

Este projeto é mantido com auxílio do **Claude (Anthropic)**.

### Trabalhando com Claude Code

1. Leia o arquivo [`CLAUDE.md`](CLAUDE.md) - contém **TODO** o contexto do projeto
2. Consulte [`docs/PROMPTS-CLAUDE-CODE.md`](docs/PROMPTS-CLAUDE-CODE.md) para templates prontos
3. Sempre atualize o `CHANGELOG.md` ao fazer mudanças

### Padrões de Desenvolvimento

- ✅ **Edições cirúrgicas** (use `str_replace`, não reescreva tudo)
- ✅ **Sincronizar arquivos** após cada mudança
- ✅ **Atualizar documentação** sempre
- ✅ **Mostrar preview** antes de mudanças visuais

---

## 📈 Versão Atual

**v1.1.0** (28/04/2026)

### Novidades Recentes
- ✨ Filtro dinâmico de pontos
- ✨ Toggle "Mostrar Todos os Pontos"
- ✨ Gráfico Misto (Barras + Linha Total)
- 🔧 Melhorias de UX na aba Evolução

📜 [Ver histórico completo](CHANGELOG.md)

---

## 📞 Suporte

- 📖 [Documentação completa](docs/)
- 🐛 [Reportar bugs](../../issues)
- 💡 [Sugerir melhorias](../../issues)

---

## 📄 Licença

Este projeto está sob a [Licença MIT](LICENSE) - veja o arquivo para detalhes.

---

## 🙏 Créditos

Desenvolvido por **Wallacy** com auxílio do **Claude (Anthropic)**.

---

**🎯 Dashboard pronto para uso. Documentação pronta para Claude Code. Ajustes futuros sem perder contexto!**

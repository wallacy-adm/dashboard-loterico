# 📥 Instalação e Uso

## 🎯 **Requisitos do Sistema**

### **Navegador:**
- Google Chrome 90+ (recomendado)
- Mozilla Firefox 88+
- Microsoft Edge 90+
- Safari 14+

### **Arquivo de Dados:**
- Microsoft Excel (.xlsx)
- Estrutura de 6 planilhas específicas
- Dados a partir de janeiro/2026 para despesas

### **Conexão Internet:**
- Necessária apenas na primeira abertura (carregamento de CDNs)
- Após cache, funciona offline

---

## 🚀 **Instalação**

### **Opção 1: Download Direto**

1. **Baixe o arquivo**
   ```bash
   # Clone o repositório
   git clone https://github.com/seu-usuario/dashboard-gerencial.git
   
   # OU baixe apenas o HTML
   wget https://github.com/seu-usuario/dashboard-gerencial/raw/main/dashboard.html
   ```

2. **Abra o arquivo**
   - Dê duplo-clique em `dashboard.html`
   - OU arraste para o navegador
   - OU clique com botão direito → "Abrir com" → Navegador

### **Opção 2: Servidor Local (Opcional)**

```bash
# Python 3
python -m http.server 8000

# Node.js
npx http-server

# Acesse: http://localhost:8000/dashboard.html
```

---

## 📊 **Preparando seus Dados**

### **1. Estrutura do Excel**

Seu arquivo Excel deve ter **exatamente** 6 planilhas (abas):

| Nome da Aba | Descrição |
|-------------|-----------|
| `vendas` | Dados de faturamento |
| `dezena` | Custos de dezena |
| `comissao_jb` | Comissões produto JB |
| `comissao_le` | Comissões produto LE |
| `comissao_bg` | Comissões produto BG |
| `aluguel` | Custos fixos de aluguel |

📖 **Veja detalhes**: [ESTRUTURA-DADOS.md](ESTRUTURA-DADOS.md)

### **2. Colunas Obrigatórias**

**Planilha `vendas`:**
```
ano | mes | rota | codigo | jb | le | bg | cn
```

**Planilhas de comissão:**
```
ano | mes | rota | codigo | comissao
```

**Planilha `dezena`:**
```
ano | mes | rota | codigo | jb | le | bg | cn
```

**Planilha `aluguel`:**
```
codigo | valor
# OU (formato com data - híbrido suportado)
ano | mes | codigo | valor
```

---

## 🎮 **Como Usar**

### **Passo 1: Carregar Dados**

1. Abra o dashboard no navegador
2. Clique no botão vermelho **"🔄 Trocar Arquivo"** (canto superior direito)
3. Selecione seu arquivo Excel (.xlsx)
4. Aguarde o processamento (aparecerá uma mensagem de sucesso)

**⚠️ Importante:**
- O arquivo é processado localmente (não é enviado para nenhum servidor)
- Seus dados ficam apenas no seu navegador
- Para trocar de arquivo, clique novamente em "Trocar Arquivo"

### **Passo 2: Navegar pelas Abas**

**📈 Aba Vendas:**
- Análise de faturamento
- Filtros: Ano, Mês, Produto, Rota, Ponto
- Visualizações: Geral, Por Produto, Por Rota, Por Ponto

**💰 Aba Despesas:**
- Breakdown: Comissão + Dezena + Aluguel
- Toggle "Excluir Comissões" (análise sem comissão)
- Status de custo (Ideal, Atenção, Crítico)
- TOP 5 Melhor Custo / Maior Despesa

**🔄 Aba Comparativo:**
- Selecione Período A (ano/mês)
- Selecione Período B (ano/mês)
- Escolha: Vendas ou Despesas
- Escolha tipo: Geral, Por Produto, Por Rota, Por Ponto
- Veja variação % e diferença R$

**📊 Aba Evolução:**
- Selecione período "De" → "Até"
- Veja gráfico temporal
- Cards: Período Inicial, Final, Variação Total, Picos
- Suporta análise de vendas e despesas simultaneamente

### **Passo 3: Filtrar Dados**

**Filtros Disponíveis:**
- ✅ **Ano**: Todos os anos presentes nos dados
- ✅ **Mês**: Ordem cronológica (jan, fev, mar...)
- ✅ **Produto**: Todos, JB, LE, BG, CN
- ✅ **Rota**: Todas ou específica (2201, 2204...)
- ✅ **Ponto**: Todos ou específico (220101, 220822...)

**💡 Dica:** Filtros são dinâmicos! As opções mudam conforme sua seleção.

### **Passo 4: Exportar Relatório**

1. Configure os filtros desejados
2. Clique em **"🖨️ Imprimir / Salvar PDF"**
3. Na janela de impressão:
   - Escolha "Salvar como PDF"
   - Ajuste layout (Paisagem recomendado)
   - Clique em "Salvar"

---

## 🔧 **Funcionalidades Especiais**

### **Toggle "Excluir Comissões"**

**Onde:** Aba Despesas e Comparativo  
**O que faz:** Remove comissões do cálculo, mostrando apenas Dezena + Aluguel  
**Quando usar:** Para análise de custos fixos/variáveis sem comissões

**Exemplo:**
```
COM comissão:
Despesas = R$ 10.000 (Comissão: R$ 3k, Dezena: R$ 5k, Aluguel: R$ 2k)

SEM comissão:
Despesas = R$ 7.000 (Dezena: R$ 5k, Aluguel: R$ 2k)
```

### **Cores e Indicadores**

**Sistema de Cores:**
- 🔴 **Vermelho**: Valores negativos
- 🟢 **Verde**: Valores positivos
- 🟡 **Amarelo**: Atenção (custo 25-35%)
- 🔴 **Vermelho**: Crítico (custo >35%)

**Status de Custo (Despesas):**
- ✅ **Ideal**: < 25% das vendas
- ⚠️ **Atenção**: 25% - 35% das vendas
- 🆘 **Crítico**: > 35% das vendas

### **Filtros Dinâmicos**

Os filtros se adaptam ao contexto:

**Exemplo - Comparativo:**
```
1. Seleciona Período A: jan/2026
2. Seleciona Período B: fev/2026
3. Filtro "Rota" mostra apenas rotas com dados em jan OU fev
4. Seleciona Rota: 2201
5. Filtro "Ponto" mostra apenas pontos da rota 2201
```

---

## ❓ **Problemas Comuns**

### **"Erro ao processar arquivo"**

**Possíveis causas:**
- ❌ Arquivo não é .xlsx
- ❌ Faltam planilhas obrigatórias
- ❌ Nomes de colunas incorretos
- ❌ Formato de dados inválido

**Solução:**
- Verifique a estrutura em [ESTRUTURA-DADOS.md](ESTRUTURA-DADOS.md)
- Use o template de exemplo em `/exemplos/template-dados.xlsx`

### **"Comparação de despesas disponível apenas para períodos ≥ 2026"**

**Causa:**
- Período A ou B anterior a 2026

**Solução:**
- Dados de despesas estão disponíveis apenas a partir de jan/2026
- Para períodos anteriores, use apenas análise de Vendas

### **Filtros não aparecem ou estão vazios**

**Causa:**
- Sem dados para o período selecionado

**Solução:**
- Verifique se há dados no Excel para aquele ano/mês
- Tente "Todos" nos filtros primeiro

### **Gráfico não carrega**

**Causa:**
- Conexão internet necessária na primeira vez (CDN Chart.js)

**Solução:**
- Aguarde carregamento completo da página
- Verifique conexão internet
- Recarregue a página (F5)

---

## 💡 **Dicas de Uso**

### **Performance:**
- ✅ Arquivos até 5MB: Performance excelente
- ⚠️ Arquivos 5-10MB: Performance boa
- 🐌 Arquivos >10MB: Pode demorar alguns segundos

### **Análises Recomendadas:**

**1. Análise Mensal (Despesas):**
```
Aba: Despesas
Filtros: Ano=2026, Mês=jan, Produto=Todos
Resultado: Visão geral do mês
```

**2. Comparação Mês a Mês:**
```
Aba: Comparativo
Período A: jan/2026
Período B: fev/2026
Tipo: Geral
Resultado: Variação total
```

**3. Performance por Produto:**
```
Aba: Vendas
Tipo: Por Produto
Resultado: Ranking de produtos
```

**4. Evolução Trimestral:**
```
Aba: Evolução
De: jan/2026
Até: mar/2026
Resultado: Gráfico + tendência
```

---

## 🆘 **Suporte**

**Documentação:**
- [Estrutura de Dados](ESTRUTURA-DADOS.md)
- [Funcionalidades Detalhadas](FUNCIONALIDADES.md)

**Issues:**
- Abra uma issue no GitHub com:
  - Descrição do problema
  - Prints de tela
  - Versão do navegador

---

**✅ Pronto para começar! Qualquer dúvida, consulte a documentação completa.**

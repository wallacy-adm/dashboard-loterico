# 🚀 INSTALAÇÃO - Como Usar o Dashboard

> Guia passo a passo para começar a usar o dashboard.

---

## 📋 Pré-requisitos

### O que você precisa:
- ✅ Um navegador moderno (Chrome, Firefox, Edge)
- ✅ Suas planilhas Excel (formato .xlsx)
- ✅ **NADA MAIS!** Sem instalação, sem servidor

---

## 🚀 Como Usar (3 Passos)

### Passo 1: Baixar o Dashboard

#### Opção A: Direto do GitHub
1. Acesse o repositório
2. Clique em `dashboard.html`
3. Clique em "Raw" ou "Download"
4. Salve em uma pasta de fácil acesso

#### Opção B: Clonar repositório completo
```bash
git clone https://github.com/{seu-usuario}/{seu-repo}.git
```

### Passo 2: Abrir no Navegador

1. Localize o arquivo `dashboard.html`
2. **Duplo clique** para abrir no navegador padrão
3. Ou: clique com botão direito → "Abrir com" → escolha o navegador

### Passo 3: Carregar Suas Planilhas

1. Clique no botão **"Selecionar arquivo"**
2. Escolha sua planilha Excel (.xlsx)
3. Aguarde o processamento (alguns segundos)
4. Pronto! Análise gerada automaticamente.

---

## 📊 Estrutura das Planilhas

Sua planilha Excel deve ter **6 abas** com os seguintes nomes:

| Aba | Conteúdo |
|-----|----------|
| `vendas` | Vendas por produto |
| `dezena` | Despesa de dezenas |
| `comissao_jb` | Comissão JB |
| `comissao_le` | Comissão LE |
| `comissao_bg` | Comissão BG |
| `aluguel` | Aluguel fixo |

📖 **Detalhes completos:** [DATA-STRUCTURE.md](DATA-STRUCTURE.md)

---

## 🎯 Navegação no Dashboard

### Abas Principais:

#### 1. 💰 Vendas
- Filtros: Ano, Mês, Rota, Ponto, Produto
- Visualizações:
  - Cards de métricas
  - Tabela detalhada
  - Gráfico de distribuição

#### 2. 💸 Despesas
- Filtros sincronizados com Vendas
- Análise de custo percentual
- Sistema de alertas (verde/amarelo/vermelho)

#### 3. ⚖️ Comparativo
- Compara dois períodos
- Variações totais e por componente
- Apenas para períodos >= jan/2026

#### 4. 📈 Evolução
- Análise temporal
- Gráfico misto (barras + linha)
- Toggle "Mostrar Todos os Pontos"

---

## 🛠️ Solução de Problemas

### Problema 1: Dashboard não abre

**Sintoma:** Página em branco ou erro ao abrir.

**Soluções:**
1. Tente outro navegador (Chrome, Firefox, Edge)
2. Limpe o cache (Ctrl+Shift+Delete)
3. Verifique se o arquivo não foi corrompido (re-baixe)

### Problema 2: Planilha não é processada

**Sintoma:** Mensagem de erro ao carregar.

**Soluções:**
1. Verifique se o arquivo é .xlsx (não .xls antigo)
2. Verifique se as abas têm os nomes corretos
3. Verifique se as colunas seguem a estrutura esperada
4. Consulte [DATA-STRUCTURE.md](DATA-STRUCTURE.md)

### Problema 3: Dados incorretos

**Sintoma:** Cálculos parecem errados.

**Soluções:**
1. Abra o console (F12) para ver mensagens
2. Verifique formato dos dados (números, datas)
3. Confirme que CN não tem comissão na sua planilha
4. Códigos devem ter 6 dígitos (RRRRPP)

### Problema 4: Gráfico não aparece

**Sintoma:** Aba carrega mas gráfico não renderiza.

**Soluções:**
1. Verifique conexão com internet (CDN do Chart.js)
2. Aguarde alguns segundos (pode ser carregamento)
3. Atualize a página (F5)

### Problema 5: Filtros não funcionam

**Sintoma:** Mudar filtro não atualiza dados.

**Soluções:**
1. Atualize a página (F5)
2. Limpe cache do navegador
3. Verifique se há dados para os filtros selecionados

---

## 💡 Dicas de Uso

### Para Análise Rápida:
1. Filtre por período específico
2. Compare 2 meses (Aba Comparativo)
3. Identifique pontos críticos (vermelhos)

### Para Análise Profunda:
1. Use aba Evolução para tendências
2. Ative "Mostrar Todos os Pontos"
3. Analise top 10 pontos individualmente
4. Compare com linha total

### Para Decisões Rápidas:
1. Olhe os Cards de Status (Ideal/Atenção/Crítico)
2. Identifique pontos no vermelho
3. Investigue causas (despesas altas? vendas baixas?)
4. Tome ação

---

## 🔒 Privacidade e Segurança

### Onde seus dados ficam?

✅ **TUDO FICA NO SEU COMPUTADOR**
- Nenhum dado é enviado para servidor
- Processamento 100% local no navegador
- Você tem controle total

### O que o dashboard NÃO faz:
- ❌ Não envia dados para internet
- ❌ Não salva em nuvem
- ❌ Não compartilha com terceiros
- ❌ Não rastreia uso

### Como funciona:
1. Você escolhe o arquivo Excel
2. Browser lê o arquivo localmente
3. JavaScript processa em memória
4. Visualização gerada na sua tela
5. **Nada sai do seu computador!**

---

## 📱 Compatibilidade

### Navegadores Testados:
- ✅ Chrome 100+
- ✅ Firefox 100+
- ✅ Edge 100+
- ✅ Safari 15+
- ⚠️ Internet Explorer **NÃO SUPORTADO**

### Sistemas Operacionais:
- ✅ Windows 10+
- ✅ macOS 11+
- ✅ Linux (qualquer distro recente)
- ✅ ChromeOS

### Mobile?
- ⚠️ Funciona, mas otimizado para desktop
- Telas pequenas: visualização pode ser comprometida
- Recomendado: tela 1280x720 ou maior

---

## 🆕 Atualizações

### Como atualizar?

#### Opção A: Re-baixar arquivo
1. Acesse o repositório GitHub
2. Baixe a versão mais recente de `dashboard.html`
3. Substitua o arquivo antigo
4. Pronto!

#### Opção B: Git pull (se clonou)
```bash
cd {pasta-do-projeto}
git pull origin main
```

### Como saber se há atualização?

1. Confira [CHANGELOG.md](../CHANGELOG.md)
2. Veja a versão atual no rodapé do dashboard
3. Compare com versão no GitHub

---

## 🤝 Suporte

### Em caso de dúvidas:

1. 📖 Consulte a [documentação](.)
2. 🐛 [Reporte bugs](../../issues)
3. 💡 [Sugira melhorias](../../issues)

---

## ✅ Checklist Inicial

Antes de começar a usar, verifique:

- [ ] Baixei o `dashboard.html`
- [ ] Tenho meu arquivo Excel (.xlsx)
- [ ] Excel tem as 6 abas com nomes corretos
- [ ] Colunas seguem a estrutura esperada
- [ ] Estou usando navegador moderno
- [ ] Tenho acesso à internet (primeira vez para CDNs)

---

**Pronto! Agora é só usar! 🚀**

---

**Última atualização:** 2026-04-28 (v1.1.0)

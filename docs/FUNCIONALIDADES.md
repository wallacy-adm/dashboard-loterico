# 🛠️ DEVELOPMENT - Guia de Desenvolvimento

> Guia completo para fazer modificações no projeto, seja você humano ou Claude Code.

---

## 🎯 Antes de Começar

### Leia primeiro (em ordem):
1. ✅ `CLAUDE.md` - Contexto geral do projeto
2. ✅ `CHANGELOG.md` - Histórico recente
3. ✅ `docs/BUSINESS-RULES.md` - Regras de negócio
4. ✅ Este arquivo (DEVELOPMENT.md)

---

## 📋 Fluxo de Trabalho Padrão

```
┌─────────────────────┐
│  1. Entender Pedido │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│  2. Localizar Código │
│  (grep + view)      │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│  3. Mostrar Preview │
│  (se for visual)    │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│  4. Aprovação?      │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│  5. Edição Cirúrgica│
│  (str_replace)      │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│  6. Sincronizar     │
│  (cp para .html)    │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│  7. Atualizar Docs  │
│  (CHANGELOG.md)     │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│  8. Reportar Status │
└─────────────────────┘
```

---

## 🔍 Como Localizar Código

### Padrão 1: Buscar Função
```bash
grep -n "function nomeDaFuncao" dashboard-COMPLETO-OTIMIZADO.html
```

### Padrão 2: Buscar Texto/Label
```bash
grep -n "Total de Vendas" dashboard-COMPLETO-OTIMIZADO.html
```

### Padrão 3: Buscar Filtro/Lógica
```bash
grep -n "filtros.evolucao" dashboard-COMPLETO-OTIMIZADO.html
```

### Padrão 4: Buscar Múltiplas Ocorrências
```bash
grep -c "filtros" dashboard-COMPLETO-OTIMIZADO.html  # Conta ocorrências
grep -n "filtros" dashboard-COMPLETO-OTIMIZADO.html | head -10  # Lista 10 primeiras
```

---

## ✏️ Como Editar Código

### REGRA DE OURO: Edições Cirúrgicas

**❌ NUNCA FAÇA:**
- Reescrever o arquivo inteiro
- Refatorar funções existentes sem pedido
- Mudar estilo/padrão de código aleatoriamente

**✅ SEMPRE FAÇA:**
- Use `str_replace` com contexto suficiente
- Mantenha o estilo do código existente
- Faça uma mudança por vez

### Exemplo: Edição Correta

```bash
# 1. Localizar
grep -n "function calcularTotal" dashboard-COMPLETO-OTIMIZADO.html
# Output: 1234:        function calcularTotal(dados) {

# 2. Ver contexto (linhas 1230-1260)
view dashboard-COMPLETO-OTIMIZADO.html [1230, 1260]

# 3. Editar com contexto
str_replace:
  old_str: "        function calcularTotal(dados) {
            return dados.reduce((s, d) => s + d.valor, 0);
        }"
  new_str: "        function calcularTotal(dados) {
            // Filtra valores válidos antes de somar
            return dados
                .filter(d => d.valor > 0)
                .reduce((s, d) => s + d.valor, 0);
        }"
```

### Cuidados com `str_replace`

#### Se der erro "não único":
```bash
# Adicione mais linhas de contexto antes/depois
old_str: "anterior contexto único
        function alvo() { ... }
        próximo contexto único"
```

#### Indentação importa!
- Use **espaços**, não tabs
- Mantenha 8 espaços de indentação dentro de funções
- Copie a indentação exata do código existente

---

## 🔄 Sincronização de Arquivos

### Após CADA modificação:

```bash
cp dashboard-COMPLETO-OTIMIZADO.html dashboard.html
```

### Por quê?
- `dashboard-COMPLETO-OTIMIZADO.html` = arquivo de trabalho
- `dashboard.html` = arquivo final (GitHub)
- Devem ser **sempre idênticos**

### Verificar sincronização:
```bash
diff dashboard-COMPLETO-OTIMIZADO.html dashboard.html
# Output vazio = arquivos idênticos ✅
```

---

## 📝 Atualizando o CHANGELOG.md

### Sempre que fizer mudanças, adicione no topo:

```markdown
## [X.Y.Z] - YYYY-MM-DD

### ✨ Adicionado
- Nova funcionalidade X

### 🔧 Melhorado
- Performance da função Y

### 🐛 Corrigido
- Bug Z na aba Comparativo
```

### Versionamento Semântico

```
MAJOR.MINOR.PATCH

MAJOR (1.x.x): Mudanças que quebram compatibilidade
MINOR (x.1.x): Novas funcionalidades (compatível)
PATCH (x.x.1): Correções de bugs
```

### Exemplos de Versão:
- `1.0.0 → 1.0.1` - Corrigiu bug
- `1.0.1 → 1.1.0` - Adicionou feature
- `1.1.0 → 2.0.0` - Mudou estrutura de dados (incompatível)

---

## 🧪 Como Testar

### Teste Manual (sempre):

1. Abrir `dashboard.html` no navegador
2. Carregar planilhas de exemplo
3. Verificar cada aba:
   - **Vendas**: Filtros funcionam? Tabela atualiza?
   - **Despesas**: Cálculos corretos? Cores certas?
   - **Comparativo**: Variações batem?
   - **Evolução**: Gráfico renderiza?

### Teste de Regressão (importante!):

Antes de finalizar, teste:
- ✅ Filtros antigos continuam funcionando
- ✅ Outras abas não quebraram
- ✅ Sem erros no console (F12)
- ✅ Performance ok (não trava com 1000+ linhas)

---

## 🚨 Erros Comuns e Soluções

### Erro 1: "str_replace falhou - múltiplas ocorrências"
**Causa:** O texto procurado existe em mais de um lugar.
**Solução:** Adicione mais contexto único antes/depois.

### Erro 2: "Indentação errada"
**Causa:** Misturou tabs e espaços, ou indentação inconsistente.
**Solução:** Sempre use 8 espaços para funções dentro de `<script>`.

### Erro 3: "Filtro não atualiza"
**Causa:** Esqueceu de chamar `render()` após mudar state.
**Solução:** Sempre `state.filtros.X = valor; render();`

### Erro 4: "Chart não atualiza"
**Causa:** Charts antigos não foram destruídos.
**Solução:** `state.charts.X.destroy()` antes de criar novo.

### Erro 5: "Dados não aparecem"
**Causa:** Estrutura da planilha diferente do esperado.
**Solução:** Verificar `docs/DATA-STRUCTURE.md`, abrir console (F12).

---

## 📊 Funções Mais Modificadas

### Top 10 funções que provavelmente vão precisar de ajustes:

| # | Função                       | Localização | Quando Mexer        |
|---|------------------------------|-------------|---------------------|
| 1 | `renderEvolucao()`           | ~2200       | Mudanças aba Evol.  |
| 2 | `criarGraficoEvolucao()`     | ~2640       | Mudanças no gráfico |
| 3 | `renderComparativo()`        | ~2000       | Mudanças aba Comp.  |
| 4 | `renderDespesas()`           | ~1500       | Mudanças aba Desp.  |
| 5 | `renderVendas()`             | ~900        | Mudanças aba Vendas |
| 6 | `getOpcoesEvolucao()`        | ~700        | Mudanças filtros    |
| 7 | `processarPlanilha()`        | ~200        | Novos formatos Excel|
| 8 | `aplicarFiltros()`           | ~800        | Lógica de filtros   |
| 9 | `calcularPontosPorPeriodo()` | ~2580       | Lógica de evolução  |
| 10| `fmt()`                      | ~150        | Formatação valores  |

⚠️ **Linhas aproximadas** - sempre confirme com `grep`.

---

## 🎨 Padrões de Estilo

### JavaScript

```javascript
// ✅ BOM
function calcularTotal(dados) {
    if (!dados || dados.length === 0) return 0;
    
    return dados.reduce((sum, item) => {
        return sum + (item.valor || 0);
    }, 0);
}

// ❌ RUIM
function calc(d) {
    return d.reduce((s,i)=>s+i.valor,0);
}
```

### HTML/JSX

```html
<!-- ✅ BOM -->
<div class="bg-white rounded-lg shadow-md p-4">
    <h2 class="text-xl font-bold mb-2">Título</h2>
    <p class="text-gray-600">Conteúdo</p>
</div>

<!-- ❌ RUIM -->
<div class="bg-white rounded p-4 shadow"><h2 class="text-xl">Título</h2><p>Conteúdo</p></div>
```

### Comentários

```javascript
// ✅ BOM - Explica O PORQUÊ
// AJUSTE 1 (v1.1.0): Filtra apenas pontos com vendas > 0 do produto
// Razão: Evitar mostrar pontos vazios no dropdown
if (filtros.produto !== 'todos') {
    dadosFiltrados = dadosFiltrados.filter(d => (d[filtros.produto] || 0) > 0);
}

// ❌ RUIM - Explica O QUE (óbvio pelo código)
// Filtra dados
dadosFiltrados = dadosFiltrados.filter(...);
```

---

## 🔧 Ferramentas Úteis

### Console do Navegador (F12)

```javascript
// Ver state completo
console.log(state);

// Ver dados de vendas
console.log(state.dados.vendas);

// Ativar logs detalhados (mude em produção)
DEBUG = true;
```

### Validação de Excel

```javascript
// No console:
ExcelJS.read(arquivo).then(wb => {
    wb.eachSheet(sheet => {
        console.log(sheet.name, sheet.rowCount);
    });
});
```

---

## 📦 Comandos Git Úteis

### Para o Wallacy (publicar mudanças):

```bash
# Ver o que mudou
git status

# Adicionar todos os arquivos modificados
git add .

# Commit com mensagem descritiva
git commit -m "feat: adiciona X na aba Y (v1.1.0)"

# Enviar para GitHub
git push origin main
```

### Padrão de Commits (Conventional Commits):

```
feat:     Nova funcionalidade
fix:      Correção de bug
docs:     Mudanças em documentação
style:    Formatação (sem mudar código)
refactor: Refatoração
perf:     Melhoria de performance
test:     Testes
chore:    Tarefas de manutenção
```

### Exemplos Bons:
```
feat: adiciona gráfico misto na aba Evolução (v1.1.0)
fix: corrige cálculo de despesas para CN
docs: atualiza CHANGELOG com v1.1.0
perf: otimiza renderização de tabela grande
```

---

## 🚀 Workflow para Claude Code

### Quando Wallacy pedir uma mudança:

```
1. Confirme o entendimento (se complexo)
   "Você quer X que faz Y, certo?"

2. Use grep para localizar
   "Vou buscar a função relevante..."

3. Use view para entender contexto
   [view com 30 linhas antes e depois]

4. Se for visual: mostre preview
   visualize:show_widget

5. Aguarde aprovação

6. Faça str_replace cirúrgico

7. Sincronize arquivos
   cp dashboard-COMPLETO-OTIMIZADO.html dashboard.html

8. Atualize CHANGELOG.md
   [adiciona nova versão]

9. Reporte status
   "✅ Pronto! Versão X.Y.Z"
```

---

## ✅ Checklist Antes de Finalizar

Antes de dizer "pronto" para o Wallacy:

- [ ] Modificação foi cirúrgica (não reescreveu tudo)
- [ ] Testou mentalmente o fluxo
- [ ] Sincronizou os 2 arquivos HTML
- [ ] Atualizou CHANGELOG.md
- [ ] Atualizou versão se necessário
- [ ] Não quebrou outras funcionalidades
- [ ] Documentou no commit (se aplicável)
- [ ] Reportou status claro ao Wallacy

---

**Última atualização:** 2026-04-28 (v1.1.0)

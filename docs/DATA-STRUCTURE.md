# 📜 CONTEXT - Contexto Histórico do Projeto

> Histórico completo do projeto, decisões tomadas, preferências do Wallacy e lições aprendidas.

---

## 👤 Sobre o Wallacy

### Background:
- **Não é programador** - sem habilidades técnicas em código
- **Conhece muito o negócio** - vendas, despesas, operações
- **Direto e objetivo** - prefere ação rápida, não teoria
- **Crítico construtivo** - questiona ideias e dá feedback honesto
- **Foco em resultados** - quer impacto mensurável

### Preferências de Comunicação:

| O que prefere ✅                  | O que NÃO prefere ❌            |
|----------------------------------|--------------------------------|
| Português brasileiro              | Inglês técnico desnecessário   |
| Estrutura visual (emojis, listas) | Texto corrido longo            |
| Tom direto                        | Floreios e clichês motivacionais|
| Foco em ação                      | Teoria sem aplicação           |
| Status claro (✅❌⏳)              | Respostas vagas                |
| Críticas construtivas             | Validação automática           |

### Estilo de Trabalho:

```
1. Pede algo específico
2. Quer ver progresso visual
3. Aprova/rejeita com clareza
4. Aprecia mockups antes de implementar
5. Valoriza economia de tokens (cirurgia, não reescrita)
```

---

## 🎯 Origem do Projeto

### Necessidade Original:
- Wallacy precisava analisar dados de vendas e despesas de jogos populares
- Múltiplas planilhas Excel separadas, difícil de cruzar manualmente
- Queria visualizações claras para tomada de decisão

### Solução Inicial:
- Script Python para processar Excel
- Limitação: precisaria instalar Python na máquina dele

### Pivot:
- Mudar para HTML/JS (roda em qualquer navegador)
- Sem instalação, sem servidor
- Wallacy só clica e usa

---

## 📅 Linha do Tempo

### Fase 1: Concepção (Início)
- Definição dos 4 produtos (JB, LE, BG, CN)
- Estrutura inicial: 4 abas (Vendas, Despesas, Comparativo, Evolução)
- Decisão: HTML/JS puro

### Fase 2: MVP (v0.x)
- Implementação inicial das abas
- Múltiplos artefatos React separados
- **Problema:** Limite de 15k caracteres por artefato no Claude.ai

### Fase 3: Migração (v1.0.0)
- Decisão: Migrar tudo para HTML único
- Tamanho final: ~3.000 linhas em 1 arquivo
- Estrutura simplificada e portátil

### Fase 4: Polimento (v1.0.x)
- Múltiplas correções de bugs
- Refinamento de UX
- Sistema de cores por sinal matemático
- Cards empilhados verticalmente

### Fase 5: Documentação GitHub (v1.0.0 final)
- README, CHANGELOG, LICENSE
- Documentação completa em `docs/`
- Pronto para publicação

### Fase 6: Refinamentos (v1.1.0)
- Filtro dinâmico de pontos
- Toggle "Mostrar Todos os Pontos"
- Gráfico misto (barras + linha)
- Documentação atualizada

### Fase 7: Migração para Claude Code (atual)
- Criação de CLAUDE.md
- Documentação adicional para Claude Code
- Templates de prompts
- Continuidade sem perda de contexto

---

## 🤔 Decisões Importantes Tomadas

### Decisão 1: HTML único (não múltiplos arquivos)
- **Quando:** Migração v1.0.0
- **Por quê:** Limite de tokens em artefatos React
- **Trade-off:** Arquivo grande, mas portátil
- **Resultado:** ✅ Funcionou bem

### Decisão 2: Sem framework JavaScript
- **Quando:** Início do projeto
- **Por quê:** Wallacy não programa, manutenção precisa ser simples
- **Trade-off:** Mais código manual, mas sem complexidade
- **Resultado:** ✅ Vanilla JS é suficiente

### Decisão 3: Chart.js (não D3.js)
- **Quando:** Início
- **Por quê:** Simplicidade vs poder
- **Trade-off:** Menos customização, mas mais fácil
- **Resultado:** ✅ Cobriu todos os casos

### Decisão 4: Cores por sinal matemático
- **Quando:** Refinamento v1.0.x
- **Por quê:** Consistência visual
- **Trade-off:** Pode parecer estranho ("despesa caindo = vermelho")
- **Resultado:** ✅ Padrão financeiro internacional

### Decisão 5: Cards verticalmente (não grid)
- **Quando:** Refinamento v1.0.x
- **Por quê:** Preferência visual do Wallacy
- **Trade-off:** Mais scroll, mas leitura sequencial melhor
- **Resultado:** ✅ Aprovado pelo Wallacy

### Decisão 6: Gráfico Misto na Evolução
- **Quando:** v1.1.0
- **Por quê:** Linhas múltiplas confusas, barras puras sem total
- **Iterações:**
  1. Múltiplas linhas → confuso ❌
  2. Barras agrupadas → boa, sem total ⚠️
  3. Heatmap → boa, mas requer "educação" ⚠️
  4. **Misto (barras + linha) → ✅ ESCOLHIDO**
- **Resultado:** ✅ Detalhe + visão macro

### Decisão 7: Top 10 Pontos no Gráfico
- **Quando:** v1.1.0
- **Por quê:** Performance e clareza visual
- **Trade-off:** Pontos > 10 não aparecem
- **Resultado:** ✅ Cobre 90%+ dos casos

### Decisão 8: Despesas a partir de Jan/2026
- **Quando:** Definição inicial
- **Por quê:** Wallacy só tem dados a partir dessa data
- **Implicação:** Aba Comparativo bloqueia períodos anteriores
- **Resultado:** ✅ Validação clara para usuário

---

## 💡 Lições Aprendidas

### Lição 1: Mostrar Antes de Implementar
- ❌ Implementar primeiro, mostrar depois → desperdiça tokens
- ✅ Mockup visual primeiro, implementar após aprovação

**Aplicação:** Sempre usar `visualize:show_widget` para mudanças visuais.

### Lição 2: Edições Cirúrgicas
- ❌ Reescrever arquivo inteiro → estoura tokens, demora
- ✅ `str_replace` com contexto → preciso e econômico

**Aplicação:** Workflow: grep → view → str_replace.

### Lição 3: Sincronização Importante
- ❌ Editar só `dashboard.html` → versão de trabalho fica defasada
- ✅ Editar `dashboard-COMPLETO-OTIMIZADO.html` → copiar para `.html`

**Aplicação:** Sempre `cp` após cada modificação.

### Lição 4: Documentar no Mesmo Sprint
- ❌ Implementar agora, documentar depois → documentação fica desatualizada
- ✅ CHANGELOG.md atualizado junto com código

**Aplicação:** Atualizar versão e changelog na mesma sessão.

### Lição 5: Wallacy Quer Críticas
- ❌ Validar tudo automaticamente → não ajuda
- ✅ Apontar riscos, problemas, alternativas → agrega valor

**Aplicação:** Ser conselheiro estratégico, não yes-man.

### Lição 6: Visual > Texto
- ❌ Explicar com palavras → custa tokens, não fica claro
- ✅ Mostrar com mockup visual → comunicação rápida e clara

**Aplicação:** `visualize:show_widget` para qualquer mudança visual.

---

## 🎨 Padrões Visuais Definidos

### Cores Primárias:
```
Roxo:     #8b5cf6 (cor principal)
Verde:    #10b981 (sucesso/positivo)
Amarelo:  #f59e0b (atenção)
Vermelho: #dc2626 (crítico/negativo)
Azul:     #3b82f6 (informação)
```

### Tipografia:
- Tailwind padrão (Inter ou system fonts)
- Tamanhos: text-sm, text-base, text-lg, text-xl, text-2xl, text-3xl
- Pesos: font-normal, font-medium, font-semibold, font-bold

### Spacing:
- Padding cards: `p-4`, `p-6`
- Gap entre cards: `space-y-3`, `gap-4`, `gap-6`
- Margens: `mb-2`, `mb-4`, `mb-6`

### Cards:
```html
<div class="bg-white rounded-lg shadow-md p-4">
    <h3 class="text-lg font-semibold mb-2">Título</h3>
    <p class="text-gray-600">Conteúdo</p>
</div>
```

---

## 🚀 Próximos Passos (Roadmap Mental)

### Curto prazo (próximas iterações):
- ☐ Validar gráfico misto v1.1.0 com dados reais
- ☐ Coletar feedback do uso real
- ☐ Refinamentos baseados em uso

### Médio prazo (futuras versões):
- ☐ Possível: Exportar relatórios em PDF
- ☐ Possível: Compartilhamento de dashboards
- ☐ Possível: Histórico de análises salvas

### Longo prazo (visão):
- ☐ Possível: Integração com APIs externas
- ☐ Possível: Multi-usuário com permissões
- ☐ Possível: Dashboards customizáveis

⚠️ **Nada decidido!** Wallacy decide o roadmap conforme necessidade.

---

## 🔧 Ferramentas Usadas

### Para Desenvolvimento:
- ✅ **Claude (Anthropic)** - IA assistente
- ✅ **Claude Code** - Para edições no GitHub
- ✅ **Editor de texto** - Para visualização
- ✅ **Navegador** - Para teste

### Para Distribuição:
- ✅ **GitHub** - Hospedagem do código
- ✅ **Email/Pendrive** - Distribuição direta

---

## 📝 Convenções do Projeto

### Nomenclatura:
- **Funções:** camelCase (`renderEvolucao`, `calcularTotal`)
- **Variáveis:** camelCase (`totalVendas`, `filtroProduto`)
- **Constantes:** UPPER_SNAKE_CASE (`ORDEM_MESES`, `DEBUG`)
- **CSS:** kebab-case (`bg-white`, `text-gray-600`)

### Comentários:
```javascript
// AJUSTE X (vY.Z): Breve descrição
// Razão: Por que essa mudança foi feita
codigo_aqui;
```

### Versionamento:
- Semantic Versioning (MAJOR.MINOR.PATCH)
- Tag em CHANGELOG.md sempre

---

## 🎯 Princípios Norteadores

1. **Simplicidade > Complexidade** - Sempre que possível
2. **Wallacy First** - Decisões baseadas no usuário, não em "boas práticas" abstratas
3. **Cirurgia > Reescrita** - Edições mínimas e precisas
4. **Mostrar > Explicar** - Mockups antes de código
5. **Documentar > Memorizar** - Tudo no GitHub para continuidade
6. **Honesto > Agradável** - Críticas construtivas valem mais que validação

---

## 💬 Frases Marcantes do Wallacy

(Útil para entender expectativas)

> "ajustes cirurgicos, foco total nos ajustes!"

> "achei q ficou um pouco confuso"

> "Prezo pela responsabilidade e economia de tokens"

> "pensa mentalmente antes de tudo"

> "deixe no ponto de eu so jogar la na repo"

**Lição:** Wallacy valoriza eficiência, clareza e ação direta.

---

**Última atualização:** 2026-04-28 (v1.1.0)

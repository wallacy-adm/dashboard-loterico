# 🤖 PROMPTS-CLAUDE-CODE - Templates de Prompts

> Templates prontos de prompts para usar com Claude Code. Copie, cole, e adapte conforme necessário.

---

## 🎯 Como Usar Este Arquivo

1. Encontre o template que combina com o que você quer fazer
2. Copie o prompt
3. Cole no Claude Code
4. Adapte os campos `{em chaves}` com suas informações
5. Envie!

---

## 📌 Prompt Inicial (PRIMEIRA VEZ)

**Use isso na primeira interação com Claude Code:**

```
Olá Claude! Vou trabalhar no projeto "Dashboard Gerencial".

Antes de qualquer coisa:
1. Leia o arquivo CLAUDE.md (contém TODO o contexto)
2. Leia o CHANGELOG.md (histórico recente)
3. Confirme que entendeu

Depois disso, vou te passar a tarefa específica.
```

---

## 🐛 Correção de Bugs

### Bug Geral:

```
Encontrei um bug no dashboard:

DESCRIÇÃO: {descreva o problema}
ABA AFETADA: {Vendas/Despesas/Comparativo/Evolução}
COMO REPRODUZIR: {passos para reproduzir}
COMPORTAMENTO ESPERADO: {o que deveria acontecer}

Por favor:
1. Localize a causa do bug
2. Faça correção cirúrgica (str_replace, não reescreva)
3. Sincronize os arquivos (cp)
4. Atualize CHANGELOG.md (versão patch)
```

### Bug em Cálculo:

```
Bug em cálculo:

ABA: {qual aba}
CÁLCULO ERRADO: {o que está calculando errado}
VALOR ESPERADO: {valor correto}
VALOR OBTIDO: {valor errado}
DADOS DE TESTE: {se relevante}

Verifique:
1. Se está respeitando regras de negócio (BUSINESS-RULES.md)
2. Se CN não está sendo somado em comissão
3. Se aluguel está sendo aplicado corretamente
4. Faça correção cirúrgica
```

### Bug Visual:

```
Bug visual no dashboard:

ABA: {qual aba}
ELEMENTO: {card/tabela/gráfico}
PROBLEMA VISUAL: {descrição}

Antes de implementar:
1. Mostre um mockup do antes/depois
2. Aguarde minha aprovação

Depois implementar cirurgicamente.
```

---

## ✨ Adicionar Funcionalidade

### Nova Feature:

```
Quero adicionar uma nova funcionalidade:

DESCRIÇÃO: {o que quer adicionar}
ABA: {onde vai ficar}
COMO DEVE FUNCIONAR: {detalhes}
POR QUÊ: {motivação/caso de uso}

Por favor:
1. Faça perguntas se algo não estiver claro
2. Mostre mockup visual antes de implementar
3. Aguarde minha aprovação
4. Implemente cirurgicamente
5. Atualize CHANGELOG.md (versão minor)
6. Sincronize arquivos
```

### Novo Filtro:

```
Adicionar novo filtro:

ABA: {qual aba}
TIPO DE FILTRO: {dropdown/checkbox/range}
VALORES POSSÍVEIS: {lista de opções}
LÓGICA: {como deve filtrar os dados}

Verifique:
1. Se o filtro deve afetar tabelas E cards (geralmente sim)
2. Se deve esconder registros vazios
3. Se interage com outros filtros existentes

Mostre como ficará na UI antes de implementar.
```

### Novo Card/Métrica:

```
Adicionar novo card:

ABA: {qual aba}
MÉTRICA: {o que mostra}
CÁLCULO: {fórmula}
POSIÇÃO: {onde fica}

Lembre-se:
- Cor por sinal matemático (negativo=vermelho, positivo=verde)
- Cards stack verticalmente (space-y-3)
- Mantenha estilo visual consistente
```

### Novo Gráfico:

```
Adicionar novo gráfico:

TIPO: {linha/barras/pizza/misto}
ABA: {qual aba}
DADOS: {o que mostrar}

ANTES DE IMPLEMENTAR:
1. Mostre mockup visual
2. Aguarde aprovação

Use Chart.js (já está no projeto).
Use cores da paleta padrão (consulte CLAUDE.md).
```

---

## 🎨 Modificações Visuais

### Mudar Cor:

```
Mudar cor de {elemento}:

ELEMENTO: {qual elemento}
COR ATUAL: {cor atual}
COR NOVA: {cor desejada}

ANTES de implementar, confirme:
1. Está respeitando regra de cores por sinal?
2. Mantém consistência com resto do dashboard?
3. Mostre preview visual
```

### Reorganizar Layout:

```
Reorganizar layout:

ABA: {qual aba}
MUDANÇA: {o que mover/redimensionar}
RAZÃO: {por quê}

OBRIGATÓRIO:
1. Mostre mockup antes/depois
2. Aguarde aprovação
3. Mantenha cards verticais (space-y-3)
4. Faça mudanças cirúrgicas
```

### Ajustar Texto:

```
Ajustar texto/label:

ELEMENTO: {qual texto}
TEXTO ATUAL: "{texto atual}"
TEXTO NOVO: "{texto novo}"

Use grep para localizar e str_replace para mudar.
Verifique se o texto não aparece em múltiplos lugares.
```

---

## 📊 Modificações em Dados

### Adicionar Nova Coluna:

```
Adicionar coluna em planilha:

PLANILHA: {qual planilha}
NOVA COLUNA: {nome}
TIPO: {string/number/etc}
USO: {para que serve}

Verifique:
1. Atualizar DATA-STRUCTURE.md
2. Atualizar processamento da planilha
3. Atualizar validações
4. Documentar em CHANGELOG.md
```

### Mudar Validação:

```
Mudar validação de dados:

REGRA: {qual regra}
COMPORTAMENTO ATUAL: {como funciona}
COMPORTAMENTO DESEJADO: {como deveria funcionar}

Antes de implementar:
1. Verificar impacto em BUSINESS-RULES.md
2. Confirmar se é uma regra crítica
3. Mostrar plano de implementação
```

---

## 📋 Tarefas de Manutenção

### Atualizar Documentação:

```
Atualizar documentação:

ARQUIVO: {qual arquivo .md}
SEÇÃO: {qual seção}
MUDANÇA: {o que atualizar}

Mantenha estilo consistente com outros docs.
```

### Refatoração:

```
⚠️ ATENÇÃO: Refatoração pedida.

PARTE: {o que refatorar}
RAZÃO: {por quê}
OBJETIVO: {o que melhorar}

ANTES DE IMPLEMENTAR:
1. Explicar plano detalhado
2. Mostrar antes/depois (estrutural)
3. Listar riscos
4. Aguardar aprovação explícita

Refatorações são raras - questione se é realmente necessário.
```

### Performance:

```
Melhorar performance:

PROBLEMA: {o que está lento}
QUANDO ACONTECE: {situação}
OBJETIVO: {meta de melhoria}

Antes de implementar:
1. Identificar gargalo
2. Propor solução
3. Estimar impacto
4. Aguardar aprovação
```

---

## 🚀 Tarefas Específicas Comuns

### Mudar Threshold de Custo:

```
Mudar thresholds de custo percentual:

NOVO IDEAL: {< X%}
NOVO ATENÇÃO: {entre X% e Y%}
NOVO CRÍTICO: {> Y%}

Lembre que:
1. Atualizar em todos os lugares que usa
2. Atualizar BUSINESS-RULES.md
3. Atualizar CLAUDE.md
4. Cards e tabelas devem ser consistentes
```

### Adicionar Novo Produto:

```
⚠️ MUDANÇA GRANDE: Adicionar novo produto

NOVO PRODUTO: {código - 2 letras}
TEM COMISSÃO?: {sim/não}
NOME COMPLETO: {nome do produto}

OBRIGATÓRIO:
1. Atualizar TODAS as referências (procurar JB, LE, BG, CN)
2. Atualizar DATA-STRUCTURE.md
3. Atualizar BUSINESS-RULES.md
4. Atualizar CLAUDE.md
5. Atualizar planilha de exemplo
6. Versão MAJOR (incompatível com dados antigos!)

Antes de implementar, mostre plano completo.
```

### Backup de Versão:

```
Antes de fazer mudança grande, faça backup:

1. Crie cópia: dashboard-vX.Y.Z-backup.html
2. Confirme backup feito
3. Prossiga com a mudança
```

---

## 🔍 Análise/Investigação

### Investigar Problema:

```
Investigue o seguinte:

CONTEXTO: {situação}
SUSPEITA: {o que acho que pode ser}
COMPORTAMENTO ESTRANHO: {o que vejo}

Por favor:
1. Use grep para investigar o código
2. Não faça mudanças ainda
3. Reporte o que encontrou
4. Proponha soluções
```

### Auditoria de Código:

```
Faça uma auditoria de:

ÁREA: {função/aba/feature}

Verifique:
1. Está respeitando regras de negócio?
2. Tem validações adequadas?
3. Performance ok?
4. Código limpo e legível?

Reporte em formato de checklist com ✅/❌
```

---

## 📦 Build/Deploy

### Sincronizar Arquivos:

```
Sincronize os arquivos:

cp dashboard-COMPLETO-OTIMIZADO.html dashboard.html

Confirme com diff que estão idênticos.
```

### Preparar Release:

```
Preparar release v{X.Y.Z}:

1. Verificar todos os arquivos atualizados
2. Confirmar CHANGELOG.md tem nova versão
3. Atualizar versão em README.md
4. Atualizar data em CLAUDE.md
5. Sincronizar arquivos HTML
6. Listar tudo que mudou
7. Sugerir mensagem de commit
```

---

## 🎓 Aprendizado/Exploração

### Explicar Código:

```
Explique como funciona:

ARQUIVO: {qual}
FUNÇÃO: {qual função}

Por favor:
1. Explicar em português, simples
2. Sem jargão técnico desnecessário
3. Com exemplos práticos
4. Em formato de lista/seções
```

### Mostrar Estrutura:

```
Me mostre a estrutura de:

ÁREA: {função/aba/módulo}

Use diagrama ASCII ou texto estruturado.
Foque no que é relevante, não em todos os detalhes.
```

---

## 💡 Dicas Gerais

### Para qualquer prompt:

✅ **SEMPRE inclua:**
- Contexto claro
- Objetivo específico
- Critérios de aceitação

✅ **PEÇA explicitamente:**
- Mockup antes de implementar (se visual)
- Aprovação antes de mudanças grandes
- Atualização de documentação
- Sincronização de arquivos

✅ **EVITE:**
- Pedidos vagos ("melhora isso aí")
- Múltiplas tarefas no mesmo prompt
- Pular passo de aprovação

---

## 🚨 Comandos de Emergência

### Reverter Mudança:

```
Reverter última mudança:

A última modificação no arquivo {qual} causou problema.

Por favor:
1. Identificar o que foi mudado
2. Reverter usando str_replace (forma cirúrgica)
3. Confirmar que voltou ao estado anterior
4. Sincronizar arquivos
```

### Verificar Integridade:

```
Verifique integridade do projeto:

1. Os 2 arquivos HTML são idênticos?
2. Todas as funcionalidades funcionam?
3. CHANGELOG.md está atualizado?
4. Documentação está consistente?

Reporte em checklist.
```

---

## 📞 Quando Pedir Ajuda

### Use estes prompts quando estiver perdido:

```
Não sei como fazer {X}. Pode me orientar?

Considere:
- Não sou programador
- Quero entender o que vai mudar
- Prefiro começar simples e ir refinando
```

```
Tenho um objetivo: {descrever objetivo}.

Não sei a melhor abordagem. Por favor:
1. Liste 2-3 opções possíveis
2. Compare prós e contras
3. Me ajude a decidir
4. Não implemente ainda
```

---

**Última atualização:** 2026-04-28 (v1.1.0)

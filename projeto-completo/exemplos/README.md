# 📊 Planilhas de Exemplo

Esta pasta deve conter planilhas Excel de exemplo para testar o dashboard.

## ⚠️ Importante

**NÃO comite dados reais aqui!** Use apenas dados fictícios/exemplos.

## 📋 Estrutura Esperada

Crie um arquivo `exemplo.xlsx` com 6 abas:

### Aba 1: vendas
```
| codigo | rota | jb     | le     | bg     | cn     | mes | ano  |
|--------|------|--------|--------|--------|--------|-----|------|
| 220505 | 2205 | 5000   | 3000   | 2000   | 1500   | jan | 2026 |
```

### Aba 2: dezena
```
| codigo | valor | mes | ano  |
|--------|-------|-----|------|
| 220505 | 200   | jan | 2026 |
```

### Abas 3-5: comissao_jb, comissao_le, comissao_bg
```
| codigo | valor | mes | ano  |
|--------|-------|-----|------|
| 220505 | 500   | jan | 2026 |
```

### Aba 6: aluguel (sem mes/ano!)
```
| codigo | valor |
|--------|-------|
| 220505 | 100   |
```

## 📚 Documentação Completa

Para detalhes da estrutura de dados, consulte:
[../docs/DATA-STRUCTURE.md](../docs/DATA-STRUCTURE.md)

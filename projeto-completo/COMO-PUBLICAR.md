# 🚀 COMO PUBLICAR NO GITHUB

> Passo a passo simples para subir todo o projeto no seu repositório GitHub.

---

## 📋 O Que Você Tem Aqui

Esta pasta contém **TUDO** pronto para ir pro GitHub:

```
projeto-completo/
├── 📄 README.md                    # Visão geral do projeto
├── 🤖 CLAUDE.md                    # ⭐ ARQUIVO CRUCIAL - Claude Code lê automaticamente!
├── 📜 CHANGELOG.md                 # Histórico de versões
├── 📄 LICENSE                      # Licença MIT
├── 🔒 .gitignore                   # Arquivos a ignorar
├── 🎯 dashboard.html               # Arquivo principal (USAR ESTE)
├── 🔧 dashboard-COMPLETO-OTIMIZADO.html  # Cópia de trabalho
│
├── 📁 docs/
│   ├── ARCHITECTURE.md             # Decisões técnicas
│   ├── DEVELOPMENT.md              # Guia de desenvolvimento
│   ├── BUSINESS-RULES.md           # Regras de negócio
│   ├── DATA-STRUCTURE.md           # Estrutura das planilhas
│   ├── CONTEXT.md                  # Histórico do projeto
│   ├── INSTALACAO.md               # Como instalar/usar
│   ├── FUNCIONALIDADES.md          # Detalhes das abas
│   └── PROMPTS-CLAUDE-CODE.md      # ⭐ Templates para Claude Code
│
└── 📁 exemplos/
    └── README.md                   # Como criar planilhas de exemplo
```

---

## 🎯 Opção 1: Subir via Interface do GitHub (MAIS FÁCIL)

### Passo 1: Criar repositório (se não tiver)

1. Acesse https://github.com/
2. Clique em **"New"** (botão verde)
3. Nome do repo: `dashboard-gerencial` (ou outro)
4. Descrição: "Dashboard gerencial para análise de vendas e despesas"
5. Visibilidade: **Privado** (recomendado para dados sensíveis)
6. **NÃO** marque "Initialize this repository with a README"
7. Clique em **"Create repository"**

### Passo 2: Subir os arquivos

#### 2A. Subir todos de uma vez:

1. Na página do repositório vazio, clique em **"uploading an existing file"**
2. Arraste **TODOS** os arquivos da pasta `projeto-completo/` para a página
3. Aguarde upload completar
4. Mensagem de commit: `"Initial commit - v1.1.0"`
5. Clique em **"Commit changes"**

#### 2B. Manter estrutura de pastas:

⚠️ **IMPORTANTE:** Para manter as pastas `docs/` e `exemplos/`:

1. Crie uma pasta zip da pasta `projeto-completo/`
2. Faça upload do zip via GitHub Desktop OU
3. Use a opção 2 (linha de comando) abaixo

---

## 🎯 Opção 2: Subir via Linha de Comando

### Passo 1: Abrir terminal

- **Windows:** Git Bash ou CMD
- **Mac/Linux:** Terminal

### Passo 2: Navegar até a pasta

```bash
cd caminho/para/projeto-completo
```

### Passo 3: Inicializar Git (se necessário)

```bash
git init
git branch -M main
```

### Passo 4: Adicionar arquivos

```bash
git add .
```

### Passo 5: Fazer commit

```bash
git commit -m "Initial commit - v1.1.0"
```

### Passo 6: Conectar ao GitHub

```bash
git remote add origin https://github.com/{seu-usuario}/{nome-do-repo}.git
```

⚠️ Substitua `{seu-usuario}` e `{nome-do-repo}` pelos valores reais!

### Passo 7: Enviar para GitHub

```bash
git push -u origin main
```

---

## 🎯 Opção 3: GitHub Desktop (INTUITIVO)

### Passo 1: Baixar GitHub Desktop

- https://desktop.github.com/

### Passo 2: Login

- Faça login com sua conta GitHub

### Passo 3: Adicionar repositório local

1. Menu **File → Add local repository**
2. Selecione a pasta `projeto-completo/`
3. Se aparecer "This directory does not appear to be a Git repository", clique em **"create a repository"**

### Passo 4: Publicar

1. Clique em **"Publish repository"**
2. Configure nome, descrição, privacidade
3. Clique em **"Publish Repository"**

---

## ✅ Verificação Pós-Upload

Após subir, verifique no GitHub:

- [ ] Arquivo `README.md` aparece na página principal
- [ ] Pasta `docs/` está visível
- [ ] Arquivo `CLAUDE.md` está na raiz
- [ ] `dashboard.html` está acessível
- [ ] LICENSE foi reconhecida pelo GitHub

---

## 🤖 Usando Claude Code Após Publicação

### Passo 1: Instalar Claude Code

Siga instruções em: https://docs.claude.com/

### Passo 2: Conectar ao seu repositório

```bash
cd projeto-completo
claude
```

### Passo 3: Primeiro comando

Use este prompt no Claude Code:

```
Olá Claude! Vou trabalhar no projeto "Dashboard Gerencial".

Antes de qualquer coisa:
1. Leia o arquivo CLAUDE.md (contém TODO o contexto)
2. Leia o CHANGELOG.md (histórico recente)
3. Confirme que entendeu

Depois disso, vou te passar a tarefa específica.
```

### Passo 4: Pedir mudanças

Use os templates em `docs/PROMPTS-CLAUDE-CODE.md`!

---

## 📋 Estrutura de Commits Sugerida

### Para próximas mudanças:

```bash
# Após mudanças
git add .
git commit -m "tipo: descrição (vX.Y.Z)"
git push
```

### Tipos de Commit:

| Tipo | Quando Usar |
|------|-------------|
| `feat:` | Nova funcionalidade |
| `fix:` | Correção de bug |
| `docs:` | Mudança em documentação |
| `style:` | Formatação |
| `refactor:` | Refatoração |
| `perf:` | Performance |

### Exemplos:

```bash
git commit -m "feat: adiciona filtro por categoria (v1.2.0)"
git commit -m "fix: corrige cálculo de variação na aba Comparativo (v1.1.1)"
git commit -m "docs: atualiza CHANGELOG com nova versão"
```

---

## 🔧 Troubleshooting

### Erro: "Permission denied (publickey)"

**Causa:** SSH não configurado.

**Solução:**
1. Use HTTPS em vez de SSH
2. Substitua na URL: `git@github.com:` por `https://github.com/`

### Erro: "Repository not found"

**Causa:** URL errada ou repo privado sem autenticação.

**Solução:**
1. Verifique a URL
2. Configure token de acesso pessoal:
   - GitHub → Settings → Developer settings → Personal access tokens
   - Crie token com permissão "repo"
   - Use token como senha ao fazer push

### Erro: "Updates were rejected"

**Causa:** Repositório remoto tem commits que você não tem.

**Solução:**
```bash
git pull origin main --allow-unrelated-histories
git push origin main
```

---

## 🎯 Próximos Passos Após Publicação

1. ✅ **Compartilhar** o repositório (se relevante)
2. ✅ **Adicionar README.md** para descrever o projeto
3. ✅ **Configurar GitHub Pages** (opcional - hospedagem gratuita)
4. ✅ **Adicionar tópicos** ao repo para descoberta
5. ✅ **Convidar colaboradores** (se houver)

---

## 🆘 Precisa de Ajuda?

### Recursos:
- 📖 [Docs GitHub](https://docs.github.com/pt)
- 🎓 [GitHub Learning Lab](https://lab.github.com/)
- 💬 Comunidade: Stack Overflow

### Para ajustes futuros:
- Use [`docs/PROMPTS-CLAUDE-CODE.md`](docs/PROMPTS-CLAUDE-CODE.md) com Claude Code

---

**Pronto! Seu projeto está no GitHub! 🚀**

---

**Última atualização:** 2026-04-28 (v1.1.0)

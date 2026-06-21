# GitHub Issues e Projects — abordagem recomendada

Sim: as abas **Issues** e **Projects** devem estar populadas — mas com **trabalho real de backlog**, não com ruído de Dependabot.

---

## Diagnóstico atual (Mongo-RestFull-API)

| Métrica | Valor | Interpretação |
|---------|-------|---------------|
| `open_issues_count` | 24 | Contagem inclui **PRs Dependabot** abertos |
| Issues de produto | ~0 | Aba parece vazia para quem filtra Issues |
| Projects vinculados | 0 | Project existente na conta é **VaultSpring**, outro repo |

---

## O que fazer

### 1. Separar Dependabot de Issues

```text
Dependabot PRs  →  revisar/mergear/fechar (não são backlog)
Issues            →  bugs, features, docs, débito técnico
```

Opcional: em `.github/dependabot.yml`, agrupar updates semanais para reduzir PRs abertos.

### 2. Criar labels padrão

| Label | Uso |
|-------|-----|
| `type:bug` | Correção de comportamento |
| `type:feature` | Nova funcionalidade |
| `type:docs` | Documentação |
| `type:chore` | Manutenção, deps, CI |
| `priority:high` | Bloqueia release |
| `good first issue` | Onboarding |

### 3. Usar templates de Issue

- `.github/ISSUE_TEMPLATE/bug_report.yml`
- `.github/ISSUE_TEMPLATE/feature_request.yml`

### 4. Criar GitHub Project dedicado

**Nome sugerido:** `Mongo-RestFull-API — Roadmap`

Colunas Kanban:

```text
Backlog → Ready → In Progress → In Review → Done
```

Itens iniciais sugeridos (criar como Issues):

1. `docs: README e CONTRIBUTING alinhados ao código` (esta entrega)
2. `chore: triagem PRs Dependabot abertos`
3. `fix: alinhar license package.json (MIT)`
4. `feat: deploy real ou remover job mock do CI`
5. `docs: corrigir SECURITY.md`

Vincular Issues ao Project: **Projects → Add item → Repository issues**.

### 5. Fluxo de trabalho

```text
Issue → branch feature/NN-descricao → PR (fecha #NN) → Project card → Done
```

Branches sugeridas: `feature/`, `fix/`, `docs/`, `chore/` + número da issue.

---

## VaultSpring vs Mongo-RestFull-API

O prompt de auditoria menciona VaultSpring/Java Spring — **não se aplica** a este repositório.  
Mantenha **Projects separados** por produto para não misturar contextos na aba Projects.

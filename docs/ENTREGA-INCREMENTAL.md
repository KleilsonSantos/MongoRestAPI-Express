# Entrega incremental — documentação

Ordem sugerida de merge para **zero impacto** no runtime da API.

## PR 1 — Documentação core (este pacote)

**Branch:** `docs/readme-restructure`

| Arquivo | Ação |
|---------|------|
| `README.md` | Reescrita factual |
| `CONTRIBUTING.md` | Novo |
| `CHANGELOG.md` | Novo |
| `SECURITY.md` | Corrigido |
| `docs/AUDITORIA-DOCUMENTACAO.md` | Novo |
| `docs/GITHUB-ISSUES-PROJECTS.md` | Novo |
| `docs/ENTREGA-INCREMENTAL.md` | Este guia |
| `.github/PULL_REQUEST_TEMPLATE.md` | Novo |
| `.github/ISSUE_TEMPLATE/*.yml` | Novos |
| `package.json` | Apenas metadata (repository, license, bugs, homepage) |

**Validação:** nenhum arquivo em `src/` alterado.

## PR 2 — GitHub Project + Issues (manual / gh CLI)

1. Criar project `Mongo-RestFull-API — Roadmap`
2. Abrir issues iniciais (docs, dependabot, deploy CI)
3. Vincular PR 1 à issue de docs

## PR 3 — Dependabot triage (opcional)

Revisar PRs #81–#86 em lote separado; não misturar com docs.

## PR 4 — Melhorias de código (futuro)

- Deploy real ou remoção do job mock
- Swagger `info.version` sync com package.json
- Playwright E2E (se desejado) ou remover da roadmap antiga

---

## Checklist de validação (anti-alucinação)

- [x] Estrutura `src/` verificada no disco
- [x] Rotas conferidas em `router.ts`
- [x] Workflow único: `main-ci.yml`
- [x] `docker-compose.yml` existe
- [x] Versão package.json: 1.4.5
- [x] Stack: Node/TS/Express — não Java Spring

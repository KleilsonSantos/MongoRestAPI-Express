# Auditoria de documentação — Mongo-RestFull-API

**Repositório:** [KleilsonSantos/Mongo-RestFull-API](https://github.com/KleilsonSantos/Mongo-RestFull-API)  
**Data:** 2026-06-21  
**Stack real:** Node.js 18+, TypeScript, Express, MongoDB/Mongoose — **não** Java Spring / VaultSpring

---

## 1. Resumo executivo

| Área | Status | Ação |
|------|--------|------|
| README.md | Desatualizado, redundante, impreciso | Reescrita completa |
| CONTRIBUTING.md | Ausente | Criar |
| CHANGELOG.md | Ausente | Criar |
| SECURITY.md | Template genérico (versões 4.x/5.x inexistentes) | Corrigir |
| package.json metadata | URLs apontam repo antigo; license ISC vs MIT | Alinhar |
| CI documentado | README cita `ci-core.yml` + `deploy.yml` | Corrigir → `main-ci.yml` |
| Estrutura de pastas no README | Duplicada e incorreta | Corrigir com árvore real |
| Docker | README diz "criar docker-compose" | Arquivo **existe** e inclui stack observabilidade |
| GitHub Issues | 24 abertos = **Dependabot PRs**, não issues reais | Triagem + templates |
| GitHub Projects | Projeto existente é **VaultSpring**, não este repo | Criar project dedicado |

---

## 2. Lacunas e imprecisões no README anterior

### 2.1 Estrutura de diretórios (incorreta)

O README listava `src/routes/`, `user-model.ts`, middlewares duplicados em `models/`.  
**Estrutura real:**

```text
src/
├── app.ts
├── config/          # db, logger, swagger, load-env
├── controllers/     # user, movie, metrics
├── enum/
├── interfaces/
├── metrics/
├── middlewares/     # auth, error, morgan, metrics, swagger
├── model/           # User.ts, Movie.ts (singular)
├── routers/         # router.ts, api-router.ts (swagger annotations)
├── server/          # server.ts, main.ts
├── services/
├── tests/
├── types/
└── utils/
```

### 2.2 CI/CD (incorreto)

| README antigo | Realidade |
|---------------|-----------|
| `.github/workflows/ci-core.yml` | **Não existe** |
| `.github/workflows/deploy.yml` | **Não existe** |
| Deploy automatizado pós-CI | Job mock `echo "Deploying..."` em `main-ci.yml` |

Workflow existente: `.github/workflows/main-ci.yml` (build, lint, test, webpack, deploy mock).

### 2.3 Funcionalidades documentadas vs código

| Feature | Documentado | Confirmado no código |
|---------|-------------|----------------------|
| JWT auth | Sim | `auth.middleware.ts`, `generate-token.ts` |
| CRUD users/movies | Sim | Controllers + router |
| Swagger | Sim | `/api/v1/api-docs` (com auth middleware) |
| Prometheus metrics | Sim | `metrics-controller`, `prometheus.yml`, rota `/metrics` |
| Winston + Morgan | Sim | `logger.ts`, `morgan.middleware.ts` |
| Roles admin/user | Parcial | `user-role.enum.ts`; moderador em `.env` |
| Husky | Sim | `.husky/pre-commit`, `pre-push`, etc. |
| SonarQube | Sim | docker-compose + scripts; CI roda coverage |
| Playwright E2E | Marcado [x] | **Não encontrado** — testes são Jest/Supertest |
| Deploy real | Sugerido | Apenas simulado no CI |

### 2.4 Variáveis de ambiente

README listava variáveis não usadas uniformemente (`DB_NAME`, `SWAGGER_API_KEY`).  
Referência canônica: `.env.development` + `src/config/load-env.ts`.

### 2.5 Licença

- Arquivo `LICENSE`: MIT  
- `package.json`: `"license": "ISC"` → **inconsistente**

---

## 3. Arquivos correlacionados auditados

| Arquivo | Problema |
|---------|----------|
| `SECURITY.md` | Template GitHub não preenchido |
| `package.json` | `repository.url` → repo renomeado incorreto |
| `.github/workflows/main-ci.yml` | OK; não documentado corretamente |
| `docker-compose.yml` | OK; README subestimava escopo (Grafana, Sonar, Portainer) |

---

## 4. GitHub Issues e Projects

### Issues (aba vazia / confusa)

- API reporta `open_issues_count: 24`, mas `gh issue list` retorna vazio porque são **Pull Requests Dependabot** (#81–#86), não Issues de backlog.
- **Recomendação:** usar Issues para bugs/features; configurar Dependabot para agrupar ou auto-merge; criar labels e templates.

### Projects (aba não populada para este repo)

- Existe project **"VaultSpring - Development"** — outro contexto.
- **Recomendação:** criar **"Mongo-RestFull-API — Roadmap"** e vincular issues/PRs deste repositório.

Detalhes: [GITHUB-ISSUES-PROJECTS.md](./GITHUB-ISSUES-PROJECTS.md)

---

## 5. Plano de implementação incremental

| Etapa | Entrega | Impacto no runtime |
|-------|---------|-------------------|
| 1 | Esta auditoria | Nenhum |
| 2 | README reescrito | Nenhum |
| 3 | CONTRIBUTING, CHANGELOG, SECURITY, templates | Nenhum |
| 4 | Correção `package.json` metadata | Nenhum |
| 5 | Issues + Project GitHub | Processo apenas |
| 6 | PR Dependabot triage | Opcional, separado |

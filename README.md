# Mongo REST API

API REST para gerenciamento de **usuários** e **filmes**, construída com **Node.js**, **TypeScript**, **Express** e **MongoDB**.

Repositório: [github.com/KleilsonSantos/Mongo-RestFull-API](https://github.com/KleilsonSantos/Mongo-RestFull-API)

---

## Funcionalidades

- Autenticação **JWT** e rotas protegidas por middleware
- CRUD de usuários e filmes
- Documentação interativa **Swagger** em `/api/v1/api-docs`
- Logs estruturados (**Winston**) e HTTP logging (**Morgan**)
- Métricas **Prometheus** em `/api/v1/metrics`
- Testes com **Jest** e **Supertest** (cobertura + integração Sonar no CI)
- **Docker Compose** com MongoDB, observabilidade (Prometheus/Grafana) e stack SonarQube local
- **GitHub Actions** (`main-ci.yml`): build TypeScript, lint, testes, webpack
- **Husky** para hooks de commit/push

---

## Pré-requisitos

| Ferramenta | Versão mínima |
|------------|---------------|
| Node.js | 18.x (CI usa 18.x) |
| npm | 9+ |
| MongoDB | 6+ (local ou via Docker) |
| Docker + Compose | Opcional, recomendado para stack completa |

---

## Instalação e execução local

### 1. Clonar e instalar

```bash
git clone https://github.com/KleilsonSantos/Mongo-RestFull-API.git
cd Mongo-RestFull-API
npm install
```

### 2. Variáveis de ambiente

Copie e ajuste com base em `.env.development`:

```env
NODE_ENV=development
PORT=3000
LOCALHOST=http://localhost
API_URL=/api/v1
MONGODB_URI=mongodb://admin:secret@localhost:27017/admin
JWT_SECRET=sua-chave-segura
JWT_EXPIRES_IN=1h
```

Para testes: `.env.test` (carregado via `dotenv-flow` / `load-env.ts`).

### 3. Subir dependências (Docker)

```bash
npm run docker:up
```

Serviços principais:

| Serviço | URL |
|---------|-----|
| API | `http://localhost:3000` |
| MongoDB | `localhost:27017` |
| Mongo Express | `http://localhost:8081` |
| Prometheus | `http://localhost:9090` |
| Grafana | `http://localhost:3001` |
| SonarQube | `http://localhost:9000` |

> O serviço da API no Compose está comentado; em dev use `npm run dev` no host apontando para o Mongo do Compose.

### 4. Rodar a API

```bash
# Desenvolvimento (ts-node + load-env)
npm run dev

# Produção (build + node)
npm run build:ts
npm start
```

---

## Uso da API

Base URL padrão: `http://localhost:3000/api/v1`

| Método | Rota | Auth | Descrição |
|--------|------|------|-----------|
| POST | `/login` | Não | Login → JWT |
| POST | `/create/user` | Sim | Criar usuário |
| GET | `/users` | Sim | Listar usuários |
| GET | `/users/:id` | Sim | Buscar usuário |
| PUT | `/users/:id` | Sim | Atualizar usuário |
| DELETE | `/users/:id` | Sim | Remover usuário |
| POST | `/create/movie` | Sim | Criar filme |
| GET | `/movies` | Sim | Listar filmes |
| GET | `/movies/:id` | Sim | Buscar filme |
| PUT | `/movies/:id` | Sim | Atualizar filme |
| DELETE | `/movies/:id` | Sim | Remover filme |
| GET | `/metrics` | Não* | Métricas Prometheus |
| GET | `/api-docs` | Swagger auth | Documentação OpenAPI |

\* Verifique configuração de auth do Swagger em produção.

Exemplo de login:

```bash
curl -X POST http://localhost:3000/api/v1/login \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","password":"senha"}'
```

---

## Arquitetura

```text
Cliente HTTP
    │
    ▼
Express (app.ts)
    ├── Morgan / JSON parser
    ├── /api/v1 → router.ts (users, movies, metrics)
    ├── Swagger UI (/api/v1/api-docs)
    └── error.middleware.ts
            │
            ▼
    Controllers → Services → Mongoose (User, Movie)
            │
            ▼
         MongoDB
```

Pastas principais:

```text
src/
├── config/       # db, logger, swagger, load-env
├── controllers/  # HTTP handlers
├── middlewares/  # auth, errors, metrics, swagger
├── model/        # Schemas Mongoose
├── routers/      # Rotas + anotações Swagger
├── server/       # Bootstrap do servidor
├── services/     # Regras de negócio
└── tests/        # Jest (unit + integração)
```

---

## Scripts npm

| Script | Descrição |
|--------|-----------|
| `npm run dev` | Servidor em modo desenvolvimento |
| `npm run build:ts` | Compila TypeScript → `dist/` |
| `npm start` | Produção (build + sync versão Sonar) |
| `npm test` | Testes Jest |
| `npm run test:coverage:sonar` | Cobertura + reporter Sonar |
| `npm run lint` | ESLint |
| `npm run format` | Prettier |
| `npm run docker:up` / `docker:down` | Stack Docker |

---

## CI/CD

Workflow: [`.github/workflows/main-ci.yml`](.github/workflows/main-ci.yml)

Jobs: **TypeScript build** → **lint/format** → **testes + cobertura** → **webpack** → deploy simulado.

Secrets usados: `MONGODB_URI` (testes no CI).

---

## Testes

```bash
npm test
npm run test:coverage:sonar
```

Relatórios em `coverage/` (quando gerados).

---

## Contribuição

Leia [CONTRIBUTING.md](./CONTRIBUTING.md).  
Governança Issues/Projects: [docs/GITHUB-ISSUES-PROJECTS.md](./docs/GITHUB-ISSUES-PROJECTS.md).

---

## Licença

[MIT](./LICENSE) — Copyright (c) Kleilson Santos

---

## Contato

- Email: kleilson@icloud.com
- LinkedIn: [kleilson-dev-full-stack](https://linkedin.com/in/kleilson-dev-full-stack)
- GitHub: [KleilsonSantos](https://github.com/KleilsonSantos)

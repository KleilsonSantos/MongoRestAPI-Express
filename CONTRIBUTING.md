# Contribuindo

Obrigado por considerar contribuir com o **Mongo-RestFull-API**.

## Antes de começar

1. Verifique [Issues abertas](https://github.com/KleilsonSantos/Mongo-RestFull-API/issues) ou crie uma descrevendo bug/feature.
2. Para dúvidas de processo GitHub (Issues/Projects), veja [docs/GITHUB-ISSUES-PROJECTS.md](./docs/GITHUB-ISSUES-PROJECTS.md).

## Setup local

```bash
git clone https://github.com/KleilsonSantos/Mongo-RestFull-API.git
cd Mongo-RestFull-API
npm install
cp .env.development .env.development.local  # ajuste credenciais
npm run docker:up   # opcional
npm run dev
```

## Fluxo de branches

```bash
git checkout -b feature/42-minha-mudanca
# commits...
npm run lint && npm test
git push -u origin feature/42-minha-mudanca
```

Abra Pull Request para `main`. Referencie a issue: `Closes #42`.

## Padrões de código

- TypeScript strict onde aplicável
- ESLint + Prettier (`npm run lint`, `npm run format`)
- Testes para comportamento novo ou corrigido
- Husky executa hooks — não use `--no-verify` salvo exceção documentada

## Commits

Prefira [Conventional Commits](https://www.conventionalcommits.org/):

```text
feat(auth): adiciona refresh token
fix(movies): corrige validação de título vazio
docs(readme): atualiza instruções Docker
chore(deps): bump express
```

## Pull Request

- Descreva o **porquê** da mudança
- Confirme CI verde
- Atualize `CHANGELOG.md` em `[Unreleased]` quando relevante

## Reportar vulnerabilidades

Consulte [SECURITY.md](./SECURITY.md). **Não** abra issue pública para falhas de segurança.

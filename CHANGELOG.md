# Changelog

Formato baseado em [Keep a Changelog](https://keepachangelog.com/pt-BR/1.1.0/).  
Versionamento alinhado a [SemVer](https://semver.org/lang/pt-BR/).

## [Unreleased]

### Added
- Documentação reestruturada: README, CONTRIBUTING, auditoria e guia Issues/Projects
- Templates GitHub para Issues e Pull Requests

### Changed
- README alinhado à estrutura real do código e ao workflow `main-ci.yml`
- SECURITY.md com versões suportadas corretas
- Metadados `package.json` (repository, license)

## [1.4.5] - 2025-06-18

### Added
- Stack Docker Compose (MongoDB, Prometheus, Grafana, SonarQube, Portainer)
- Métricas Prometheus e middleware de monitoramento
- Cobertura de testes Jest ampliada (controllers, middlewares, utils)
- Workflow CI unificado (`main-ci.yml`)

### Changed
- Migração contínua TypeScript / ESLint flat config
- Integração SonarQube via scripts de sync de versão

## [1.0.0] - 2025-03-07

### Added
- API REST inicial: usuários, filmes, JWT, Swagger, MongoDB/Mongoose

[Unreleased]: https://github.com/KleilsonSantos/Mongo-RestFull-API/compare/v1.4.5...HEAD
[1.4.5]: https://github.com/KleilsonSantos/Mongo-RestFull-API/compare/v1.0.0...v1.4.5
[1.0.0]: https://github.com/KleilsonSantos/Mongo-RestFull-API/releases/tag/v1.0.0

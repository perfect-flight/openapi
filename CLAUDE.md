# CLAUDE.md

Documentação pública da API da Perfect Flight, exposta para clientes em
https://docs.perfectflight.com.br (GitHub Pages, domínio em `CNAME`).

## O que é

- **`openapi.yaml`** — a fonte única da verdade. Spec OpenAPI 3.0.4. É o único
  arquivo que você edita à mão.
- **`index.html`** — saída gerada (Redoc, ~480KB). **Nunca edite à mão**; é
  regenerado pelo build e commitado no repo.

## Antes de editar

Leia o [`CONTRIBUTING.md`](CONTRIBUTING.md) e siga o que está lá: o fluxo de
trabalho (build → PR → publicação), a validação (lint) e as convenções do spec
(header `x-pf-correlation-id`, respostas de erro padronizadas, reuso de
componentes via `$ref`). É a fonte canônica — não duplique aqui.

Pontos que não podem regredir:

- Sempre rode `npm run build` e commite `openapi.yaml` + `index.html` no mesmo PR.
- `npm run lint` deve passar **limpo** (zero erros e warnings); não regrida isso.
- Não altere as versões: `info.version` e a do `package.json` ficam **fixas em
  `1.0.0`**.

## Versão e release

`info.version` e a versão do `package.json` são **fixas em `1.0.0`** (estratégia
da Redocly) — não as altere. As releases são automáticas: no merge à `main`, o
workflow [`release.yml`](.github/workflows/release.yml) calcula a tag semver a
partir dos commits ([Conventional Commits](https://www.conventionalcommits.org):
`fix:`→patch, `feat:`→minor, `feat!:`/`BREAKING CHANGE:`→major) e cria o GitHub
Release com as notas do `## [Unreleased]` do `CHANGELOG.md`. **Escreva os commits
no formato convencional.**

Mantenha o [`CHANGELOG.md`](CHANGELOG.md) (Keep a Changelog) só com o que importa
ao cliente, em `## [Unreleased]`. Rascunhe com o skill **`changelog-generator`**
seguindo o [`CHANGELOG_STYLE.md`](CHANGELOG_STYLE.md). Após a release, mova o
`## [Unreleased]` para uma seção versionada com a tag criada.

Node 22 (`.nvmrc`). Sem testes; a verificação é o lint.

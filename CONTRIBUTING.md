# Contribuindo

> Pull requests são aceitos apenas de **colaboradores da Perfect Flight**.

A documentação é **gerada** a partir de [`openapi.yaml`](openapi.yaml) (OpenAPI
3.0.4), a fonte única da verdade. O [`index.html`](index.html) é a saída do
build (Redoc) e **nunca deve ser editado à mão**.

## Pré-requisitos

- Node 22 (veja [`.nvmrc`](.nvmrc) — rode `nvm use`).
- `npm install`.

## Fluxo de trabalho

1. Edite `openapi.yaml`.
2. `npm run lint` e `npm run build` → valida o spec e regenera o `index.html`.
3. Se a mudança importar ao cliente, atualize o `CHANGELOG.md`
   (veja [Versão e release](#versão-e-release)).
4. Commite no mesmo PR, com mensagem em
   [Conventional Commits](https://www.conventionalcommits.org) — é o que define o bump.
5. Ao fazer merge na `main`, o GitHub Pages publica em
   [docs.perfectflight.com.br](https://docs.perfectflight.com.br) e a
   tag/release é criada automaticamente.

## Diagramas

Os diagramas da doc têm a fonte em [`diagrams/`](diagrams/) (Mermaid, `.mmd`) e a
imagem gerada em [`assets/`](assets/) (`.svg`, referenciada no `openapi.yaml`).
Edite o `.mmd`, **nunca** o `.svg`, e regenere:

```sh
npm run diagrams
```

Commite o `.mmd` e o `.svg` atualizados no mesmo PR. (`assets/` guarda só o que é
servido junto ao `index.html`; a fonte fica fora dele.)

## Validação

Antes de buildar, rode o lint:

```sh
npm run lint
```

O lint deve passar **limpo** (zero erros e zero warnings). Mantenha assim — se
sua mudança introduzir algum, corrija antes de abrir o PR.

## Convenções do spec

Ao adicionar ou editar endpoints, siga os padrões já existentes:

- Toda operação tem `tags`, `security: [- auth: []]` e o parâmetro de header
  `x-pf-correlation-id` (na request e ecoado como header em cada response).
- Respostas de erro padronizadas em todo endpoint: `401`
  (`UnauthorizedException`), `403` (`ForbiddenException`), `500`
  (`InternalServerErrorException`), além das específicas (`400`, `404`, `422`).
- Schemas de exceção seguem o formato `{ error, message }`.
- Reuse via `$ref: "#/components/schemas/..."`. Componentes comuns já existem:
  `CorrelationHeader`, `PageQueryParameter`, `PageSizeQueryParameter`,
  `WithDeletedQueryParameter`. Não duplique — reaproveite.
- Auth é OAuth2 `clientCredentials` (M2M). Servers: sandbox e produção sob `/v1`.

## Versão e release

A versão da API (`info.version` no `openapi.yaml`) e a do `package.json` são
**fixas em `1.0.0`**, conforme a [estratégia de versionamento da
Redocly](https://redocly.com/docs-legacy/api-registry/resources/versioning-strategies).
Não as altere a cada mudança.

O versionamento de releases é **automático**. No merge à `main`, o workflow
[`release.yml`](.github/workflows/release.yml) calcula a próxima tag
[semver](https://semver.org) a partir dos commits, cria `vX.Y.Z` e o GitHub
Release com as notas curadas do `## [Unreleased]` do CHANGELOG (fallback: o
changelog dos commits). O nível do bump vem das mensagens de commit
([Conventional Commits](https://www.conventionalcommits.org)):

- `fix: …` → **patch**
- `feat: …` → **minor**
- `feat!: …` ou rodapé `BREAKING CHANGE:` → **major**
- demais tipos (`docs:`, `chore:`, …) → patch (padrão)

> Primeira tag: o workflow parte da última tag existente. Para a numeração
> começar do `1.0.0`, crie a tag base uma vez
> (`git tag v1.0.0 && git push origin v1.0.0`); os próximos releases seguem
> `v1.0.1`, `v1.1.0`, … conforme os commits.

O [`CHANGELOG.md`](CHANGELOG.md) (formato [Keep a
Changelog](https://keepachangelog.com/en/1.1.0/)) é mantido à parte, só com o que
importa ao cliente, acumulando em `## [Unreleased]`. Use o skill
**`changelog-generator`** para rascunhar entradas a partir dos
[Conventional Commits](https://www.conventionalcommits.org) desde a última tag,
seguindo o [`CHANGELOG_STYLE.md`](CHANGELOG_STYLE.md) (mapeia tipo de commit →
seção). Esse `## [Unreleased]` vira o corpo do release; após publicar, role-o
para uma seção versionada com a tag criada.

### Atualizar a skill `changelog-generator`

A skill foi **copiada** para [`.claude/skills/`](.claude/skills/) (não há
auto-update). Para puxar a versão nova do upstream, rode o comando abaixo e
**reaplique o rodapé "Neste projeto"** no `SKILL.md`:

```sh
npx -y skills add composiohq/awesome-claude-skills --skill changelog-generator --agent claude-code
```

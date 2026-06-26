# Estilo do CHANGELOG

Guia para o skill `changelog-generator` e para quem edita o
[`CHANGELOG.md`](CHANGELOG.md). Seguimos
[Keep a Changelog 1.1.0](https://keepachangelog.com/en/1.1.0/).

## Fonte: Conventional Commits

Gere as entradas a partir dos commits desde a última tag
(`git log "$(git describe --tags --abbrev=0)"..HEAD`), seguindo
[Conventional Commits](https://www.conventionalcommits.org). Mapeie o tipo do
commit para a seção do Keep a Changelog:

| Commit                                    | Seção                                  |
| ----------------------------------------- | -------------------------------------- |
| `feat:`                                   | Added                                  |
| `fix:`                                    | Fixed                                  |
| `feat!:` / `fix!:` / `BREAKING CHANGE:`   | Changed ou Removed (marque o breaking) |
| `perf:`                                   | Changed                                |
| commit que marca depreciação              | Deprecated                             |
| correção de segurança                     | Security                               |
| `chore:` `ci:` `build:` `test:` `refactor:` `style:` `docs:` interno | **ignore** |

## Regras

- Registre só o que importa a quem consome a API; ignore o ruído interno acima.
- Acumule mudanças não lançadas em `## [Unreleased]`.
- Seções nesta ordem, só as que se aplicam: `Added`, `Changed`, `Deprecated`,
  `Removed`, `Fixed`, `Security`.
- Entradas curtas, em linguagem de cliente — não descreva implementação.
- Sem emojis. Datas em ISO (`YYYY-MM-DD`). Versões = tags de release (semver),
  não o `info.version`.
- O `## [Unreleased]` vira o corpo do GitHub Release. Após publicar, mova-o para
  `## [<tag>] - <data>` (a tag criada) e recomece um `## [Unreleased]` vazio.

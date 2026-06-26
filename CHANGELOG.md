# Changelog

Todas as mudanças relevantes desta documentação são registradas aqui.

O formato segue o [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). As
versões abaixo correspondem às tags de release (semver) criadas no merge à
`main`; a versão da API (`info.version` do `openapi.yaml`) é mantida fixa em
`1.0.0` conforme a [estratégia de versionamento da Redocly](https://redocly.com/docs-legacy/api-registry/resources/versioning-strategies).

## [Unreleased]

### Changed
- Todas as operações agora têm `operationId` e todas as tags têm descrição.
- `info` passou a declarar `license`.

### Fixed
- Exemplo de data inválido em `finishedIn` (`2024-06-31`, dia inexistente).
- Schema de `bbox` (`LayersDto`) corrigido para `array` de `number`.
- URL de contato da API.

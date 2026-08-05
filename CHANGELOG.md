# Changelog

Todas as mudanças relevantes desta documentação são registradas aqui.

O formato segue o [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). As
versões abaixo correspondem às tags de release (semver) criadas no merge à
`main`; a versão da API (`info.version` do `openapi.yaml`) é mantida fixa em
`1.0.0` conforme a [estratégia de versionamento da Redocly](https://redocly.com/docs-legacy/api-registry/resources/versioning-strategies).

## [Unreleased]

### Added
- `FieldDto` agora documenta o objeto `farm` (dados da fazenda do talhão),
  já retornado por `GET /fields/{fieldId}`, `GET /fields` e
  `GET /farms/{farmId}/fields`.
- `GET /fields/{fieldId}` agora documenta o parâmetro `withDeleted`, já
  aceito pela API.

### Fixed
- `GET /fields` e `GET /farms/{farmId}/fields` estavam documentados com
  `withDeleted`, `page` e `pageSize`, mas a API ignorava os três parâmetros;
  agora funcionam.

## [0.0.6] - 2026-08-04

### Fixed
- Enum `serviceType` de produto (`GET /suggested-products`) estava sem o valor
  `biological_application`, já presente na API.

## [0.0.5] - 2026-08-03

### Fixed
- Busca de veículos (`GET /vehicles`) corrigida e agora aceita filtros por
  `name`, `type` e `serialNumber`.

## [0.0.2] - 2026-06-26

### Added
- Guia de autenticação: passo a passo para gerar o token de acesso (OAuth2
  _client credentials_), uso de escopos, ciclo de vida do token e rotação de
  credenciais — com diagrama de sequência do fluxo.

## [0.0.1] - 2026-06-26

### Changed
- Todas as operações agora têm `operationId` e todas as tags têm descrição.
- `info` passou a declarar `license`.

### Fixed
- Exemplo de data inválido em `finishedIn` (`2024-06-31`, dia inexistente).
- Schema de `bbox` (`LayersDto`) corrigido para `array` de `number`.
- URL de contato da API.

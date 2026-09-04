# Changelog

Todas as mudanças relevantes desta documentação são registradas aqui.

O formato segue o [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). As
versões abaixo correspondem às tags de release (semver) criadas no merge à
`main`; a versão da API (`info.version` do `openapi.yaml`) é mantida fixa em
`1.0.0` conforme a [estratégia de versionamento da Redocly](https://redocly.com/docs-legacy/api-registry/resources/versioning-strategies).

## [Unreleased]

### Added
- Documentada a compressão automática de resposta (gzip/Brotli): basta o
  cliente enviar `Accept-Encoding`, o que a maioria dos clientes HTTP já faz
  por padrão.
- `GET /applications` agora documenta os parâmetros `order` (direção de
  ordenação por `createdAt`, default `asc`) e `withBoundaries` (default
  `true`; quando `false`, omite o campo `boundaries` de cada item de
  `fields`, deixando listagens grandes mais leves).
- `ApplicationDto` (`GET /applications`, `GET /applications/{applicationId}`)
  agora documenta diversos campos já retornados pela API e que faltavam na
  doc, entre eles `processedAt` e `lastReprocessedAt`, os campos de
  inspeção (`inspectionFlags`, `inspectionStatus`, `inspectionReason`,
  `inspectionObservation`, `notChargeable`, `deletedObservation`), `farms`,
  `restrictionFields`, `applicationTrack`, `runway`,
  `applicationOperationalServices`, `speedDataByGroup`, `images` e as
  variações de velocidade planejada/realizada (`plannedAverageSpeed`,
  `flowRangeVariation`, `heightRangeVariation`). Os objetos aninhados
  (`schedules`, `products`, `logs`, `serviceOrder`) também ganharam vários
  campos que a API já retorna e não estavam documentados.
- `VehicleDto` (`GET /vehicles`) agora documenta `idealHeight`,
  `idealSpeed`, `idealSwathWidth`, e os campos de integração com a nuvem do
  fabricante DGPS (`externalVehicleId`, `connector`).
- `VehicleModelDto` agora documenta o campo `type`.
- `FarmDto` (`GET /farms`) agora documenta os campos de hierarquia
  (`hasChildren`, `childrenAmount`, `parentFarmId`, `farmNameHierarchy`).
- `ProductDto`/`ProductCreatedDto` (`product`) e `SuggestedProductDto`
  (`suggested products`) agora documentam `formulation`,
  `toxicityCategory` e `colorBand`; `ProductDto`/`ProductCreatedDto` também
  passam a documentar `serviceType`.
- `AerialCompanyDto` (usado em `pilot` e `vehicle`) agora documenta `state`,
  `city` e `mapaRegistration`.

### Fixed
- `FieldDto.boundaries` estava documentado como sempre presente; corrigido
  para opcional, já que `GET /fields` pode omiti-lo (`withBoundaries=false`).
  A descrição de `boundaries` em `FieldDto` e `FarmDto` agora deixa explícito
  esse comportamento.
- `ApplicationFieldDto.boundaries` estava documentado como sempre presente;
  corrigido para opcional, já que `GET /applications` pode omiti-lo
  (`withBoundaries=false`).
- `GET /pilots` estava documentado como retornando um array de pilotos
  direto; corrigido para o formato real, uma tupla `[pilotos, total]`.
- O `type` de cada item de `layers` (`ApplicationDto.layers`) estava
  documentado com um conjunto de valores e uma convenção de nomenclatura
  (`AppliedOverlap`) diferentes dos realmente usados pela API
  (`APPLIED_OVERLAP`), e faltavam vários valores possíveis; corrigido para
  os 27 valores reais. `layers` também ganhou os campos `length`,
  `createdAt` e `updatedAt`, que já eram retornados.
- A resposta de `POST /fields` estava documentada com um `farmId` plano;
  corrigida para o formato real, que retorna `farm.id` (e `farm.customer.id`)
  aninhados.
- A resposta de `POST /seasons` agora documenta o campo `customer` aninhado,
  já retornado pela API e ausente da doc anterior.

## [0.0.8] - 2026-08-05

### Added
- `GET /fields` e `GET /farms` agora documentam o parâmetro `withBoundaries`
  (default `true`): quando `false`, omite/deixa de agregar o campo
  `boundaries` de cada item, deixando listagens grandes mais leves.

## [0.0.7] - 2026-08-04

### Added
- `FieldDto` agora documenta o objeto `farm` (`id` e `name` da fazenda do
  talhão), já retornado por `GET /fields/{fieldId}`, `GET /fields` e
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

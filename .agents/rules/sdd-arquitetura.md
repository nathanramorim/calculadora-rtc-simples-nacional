---
description: Como cumprir as diretrizes de arquitetura, pacotes por área, banco somente leitura e declaração de modelo de módulo.
globs: ["src/main/java/**", "src/main/resources/**", "sdd/spec/**"]
regras: [ARQ-01, ARQ-02, ARQ-03, ARQ-04, ARQ-05, ARQ-06, ARQ-11, ARQ-12, ARQ-13]
---

# Guia Prático — Arquitetura e Fronteiras de Módulos

Instruções operacionais para os IDs `ARQ-*` de `sdd/memory/constitution.md` (sem reproduzir o texto normativo, `GOV-04`).

## 1. Pacotes em `br.gov.serpro.rtc` (`ARQ-01`, `ARQ-02`, `ARQ-06`)
- `api/<área>`: controller, interface `*ControllerOpenApi`, service, repository, entity e dto da área (`simplesnacional`, `aliquotasimples`, `atividadesimples`, `versao`).
- `domain`: NCM, NBS, classificação tributária e validação de nomenclatura.
- `config` e `shared`: transversais, sem depender de `api`.
- Sentido do núcleo: `simplesnacional → aliquotasimples/atividadesimples`. `aliquotasimples` não importa `simplesnacional`; `atividadesimples` não importa `aliquotasimples`. `Teste_DependenciasNucleo` falha se isso for violado. A única exceção registrada é `AtividadeSimplesService → simplesnacional` (filtro por `cClassTrib`).
- Contrato novo ou alterado: anotar na interface `*ControllerOpenApi` (ADR006). Mudança incompatível pede MAJOR e ADR.

## 2. Configuração, dependências e banco (`ARQ-03`, `ARQ-04`, `ARQ-05`)
- Configuração em `application-offline.yml` (mantê-lo igual ao `application.yml` da nuvem, conforme o comentário do arquivo) com propriedades tipadas.
- Antes de nova dependência no `pom.xml`, verifique se o JDK ou o Spring já atendem.
- O banco abre com `mode=ro`. Nenhum `INSERT`, `UPDATE` ou `DELETE` no código. Mudança de dados vira script Flyway no repositório `calculadora-rtc-regime-regular` (ADR009).

## 3. Números e erros (`ARQ-12`, `ARQ-13`)
- Valores fiscais em `BigDecimal`, arredondados só por `ArredondamentoUtils` (ADR003). `Teste_ArquiteturaArredondamento` falha se houver `setScale(`, `RoundingMode` ou `MathContext` fora dela.
- A classe é idêntica à do `calculadora-rtc-regime-regular`: alterar exige alterar a cópia e as constantes SHA-256 (`Teste_ArredondamentoUtilsCopiaUnica`).
- Erro de item vira código `VSN-` catalogado e não interrompe os demais itens (ADR004, ADR010).

## 4. Declaração de modelo na Spec (`ARQ-11`)
- Toda spec traz `## Modelo do módulo`: **`enxuto`** para ajuste de dados, texto ou documentação; **`completo`** para regra de cálculo nova, mudança de contrato ou do esquema do banco.

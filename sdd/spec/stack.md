# Stack — calculadora-rtc-simples-nacional

## Dependências

| Camada | Escolha | Versão | Motivo |
|--------|---------|--------|--------|
| Linguagem | Java | 25 | ADR013 |
| Framework | Spring Boot (webmvc, restclient, security, validation, data-jpa, cache, actuator) | 4.1.2 | ADR013 |
| Banco | SQLite somente leitura (`sqlite-jdbc`, `hibernate-community-dialects`) | — | ADR001 |
| Migrações | Flyway Maven (scripts no repositório `calculadora-rtc-regime-regular`) | — | ADR009 |
| Cache | Spring Cache + Caffeine | — | ADR007 |
| API docs | springdoc-openapi-starter-webmvc-ui | 3.2.0 | ADR006 |
| Métricas | Actuator, Micrometer Prometheus (porta 9103, `/metrics`) | — | ADR008 |
| Tracing | Micrometer Tracing + OpenTelemetry | — | — |
| Utilitários | Lombok | — | — |
| Testes | spring-boot-starter-test, webmvc-test, JaCoCo | — | CI |

## Build e testes
- `./mvnw clean test jacoco:report`; JAR: `target/api-simples-nacional.jar`.
- Os testes exigem o banco gerado (perfil `testes`, `src/test/resources/application-testes.yml`).
- CI: `.github/workflows/publish-jacoco-report.yml`.
- Perfil `offline`: HTTP na porta 8082 (`/api`) e métricas na 9103.

## Layout do projeto
```
src/main/java/br/gov/serpro/rtc/
  api/simplesnacional/   controller, service (cálculo), repository, entity, collector, adapter, exceptionhandler
  api/aliquotasimples/   modelos de alíquotas por anexo e par de alíquotas
  api/atividadesimples/  atividades vigentes, Fator R (ModoFatorR)
  api/versao/            versão da aplicação e da base, comparador offline
  domain/                NCM, NBS, classificação tributária, validação de nomenclatura
  config/                cache, cors, security, JacksonConfig
  shared/                ArredondamentoUtils, serializers, ApiExceptionHandler
src/test/java/.../     testesunitarios (incl. arquitetura) e testesintegracao
docs/adr/              ADR001 a ADR013
```

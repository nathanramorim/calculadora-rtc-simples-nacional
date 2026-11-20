# Decisões — calculadora-rtc-simples-nacional

Os ADRs do projeto vivem em `docs/adr/` (fonte única). As decisões do método SDD vivem em `sdd/spec/adr/`.

## Resolvidas

| # | Decisão | Resolução | ADR |
|---|---------|-----------|-----|
| D1 | Banco | SQLite `mode=ro`, nome validado (`-pro.db` ou `-nonpro.db`) | [ADR001](../../docs/adr/ADR001-banco-sqlite-somente-leitura.md) |
| D2 | Perfil offline | Comparador de versões, `@Profile("offline")`, retry de 3 tentativas | [ADR002](../../docs/adr/ADR002-perfil-offline-e-comparador-de-versoes.md) |
| D3 | Precisão numérica | `ArredondamentoUtils`, `HALF_EVEN`, cópia idêntica à do regime-regular | [ADR003](../../docs/adr/ADR003-estrategia-de-precisao-numerica.md) |
| D4 | Erros | `ProblemDetail`, `ErrosCalculoException`, `ErroDetalhe` | [ADR004](../../docs/adr/ADR004-estrategia-de-tratamento-de-erros.md) |
| D5 | Documentação da API | SpringDoc, anotações em interfaces `*ControllerOpenApi` | [ADR006](../../docs/adr/ADR006-documentacao-api-com-springdoc.md) |
| D6 | Cache | Caffeine por `CacheSpecs` | [ADR007](../../docs/adr/ADR007-estrategia-de-cache-com-caffeine.md) |
| D7 | Métricas | Actuator + Prometheus na porta 9103 | [ADR008](../../docs/adr/ADR008-estrategia-de-metricas.md) |
| D8 | Migrações | Flyway Maven, scripts no repositório regime-regular | [ADR009](../../docs/adr/ADR009-migracoes-e-versionamento-do-banco.md) |
| D9 | Paralelismo | Threads virtuais por item | [ADR010](../../docs/adr/ADR010-processamento-paralelo-com-virtual-threads.md) |
| D10 | Fator R | Enum `ModoFatorR` derivado | [ADR011](../../docs/adr/ADR011-modelo-de-estado-do-fator-r.md) |
| D11 | Segurança e CORS | Stateless, rotas liberadas, CORS por propriedades | [ADR012](../../docs/adr/ADR012-seguranca-e-cors.md) |
| D12 | Plataforma | Spring Boot 4.1.2 e Java 25 (substitui ADR005) | [ADR013](../../docs/adr/ADR013-migracao-spring-boot-4-java-25.md) |
| D13 | Método SDD | Forge-SDD, `docs/adr/` como fonte dos ADRs do projeto | [ADR-0001](adr/adr-0001-adocao-forge-sdd.md) |

## Abertas

| # | Questão |
|---|---------|
| D14 | O ADR001 e o `application-offline.yml` citam `DatabaseValidator` e `DatabaseDownloadService`, mas nenhuma das duas classes existe em `src/`. Confirmar se foram removidas ou se faltam no repositório. |
| D15 | O `application-offline.yml` diz ser cópia do `application.yml` e cita `run-offline.sh`, e nenhum dos dois está em `src/main/resources` nem na raiz. |
| D16 | O ADR013 cita `.gitlab-ci.yml`, que não existe aqui (o CI é `.github/workflows/publish-jacoco-report.yml`). |
| D17 | `docs/adr/ADRs.md` lista ADR001 a ADR011; ADR012 e ADR013 não aparecem, e ADR005 (substituída) não está numa seção própria. |
| D18 | A `WebSecurityConfig` libera todas as rotas (`permitAll`). Definir a política para uso público. |

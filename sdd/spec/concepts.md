# Catálogo de Conceitos e Contratos (`DUP-01`) — calculadora-rtc-simples-nacional

Regra `DUP-01`: **Um conceito = uma casa.** Consulte esta tabela antes de criar entidade, módulo ou utilitário (`DUP-02`).

| Conceito | Pacote/Domínio Dono | Entidade/Classe Mestra | Contrato Público | Observação |
| --- | --- | --- | --- | --- |
| Arredondamento e escala fiscal | `shared.util` | `ArredondamentoUtils` | `MODO`, `arredondarAliquotaPublicada`, `ratearValorFiscal` | Idêntica à do regime-regular; SHA-256 conferido em teste (ADR003) |
| Cálculo do Simples Nacional | `api.simplesnacional.service` | `SimplesNacionalObservabilidadeService`, `CalculoSimplesUnificadoService` | `POST /calculadora/observabilidade/simples-nacional` | ADR010 |
| Processamento de um item | `api.simplesnacional.service` | `ProcessadorItemSimples` | estados `CALCULADO`, `NAO_CALCULADO`, erro | — |
| Escolha do par de alíquotas | `api.simplesnacional.service` | `EscolhaParAliquotasService` | `MotivoResolucaoAliquota` | Modelos em `api.aliquotasimples` |
| Erros `VSN-` | `api.simplesnacional` | `SimplesNacionalErroService`, `ErroDescricaoSimples` | `GET .../erros?codigo=` | ADR004 |
| Erro global e `ProblemDetail` | `shared.exceptionhandler` | `ApiExceptionHandler`, `ErrosCalculoException` | `ErroDetalhe` | ADR004 |
| Atividades e Fator R | `api.atividadesimples` | `AtividadeSimplesService`, `DerivacaoAnexosSimples` | `ModoFatorR` | ADR011 |
| Nomenclatura NCM e NBS | `domain.service` | `NomenclaturaService`, `ValidacaoNomenclaturaService` | `ModoValidacaoNomenclatura` | Adaptador em `api.simplesnacional.adapter` |
| Versão da aplicação e da base | `api.versao.service` | `VersaoService`, `VersaoOfflineService` | `GET /versao`, `GET /versao/status` | ADR002 |
| Cache | `config.cache` | `CaffeineCacheConfig`, `CacheSpecs` | propriedades `cache.specs` | ADR007 |
| CORS | `config.cors` | `CorsConfig`, `CorsProperties` | `app.cors.*` | ADR012 |

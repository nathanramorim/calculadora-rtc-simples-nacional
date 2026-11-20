# Módulos — calculadora-rtc-simples-nacional

Pacote raiz: `br.gov.serpro.rtc`. Sentido do núcleo verificado por `Teste_DependenciasNucleo`: `simplesnacional → aliquotasimples/atividadesimples`.

## api.simplesnacional
**Responsabilidade:** cálculo da CBS e do IBS no Simples Nacional, com observabilidade por item.
- `SimplesNacionalController` e `SimplesNacionalControllerOpenApi`.
- Serviços: `SimplesNacionalObservabilidadeService`, `SimplesNacionalCalculoService`, `CalculoSimplesUnificadoService`, `ProcessadorItemSimples`, `EscolhaParAliquotasService`, `ParametroCalculoSimplesService`, `SimplesNacionalNaoAssistidoService`.
- Erros `VSN-`: `SimplesNacionalErroService`, `ErroGlobalSimples`, `ErroDescricaoSimples`.
- Entidades e repositórios de enquadramento, regime de apuração, tipo de receita bruta, transição de alíquota em compra governamental e par de alíquotas ISS.

## api.aliquotasimples
**Responsabilidade:** modelos de alíquotas por anexo (`AliquotasAnexoSimples`, `LinhaAliquotasSimples`, `ParAliquotasSimples`) e o motivo da resolução da alíquota. Não depende de `simplesnacional`.

## api.atividadesimples
**Responsabilidade:** catálogo de atividades vigentes em uma data e estado do Fator R.
- `AtividadeSimplesService`, `DerivacaoAnexosSimples`, enum `ModoFatorR` (ADR011).
- Exceção registrada: o filtro por `cClassTrib` reutiliza a resolução do `tpRBSN` do cálculo (`AtividadeSimplesService → simplesnacional`).

## api.versao
**Responsabilidade:** `GET /versao` (todos os perfis) e `GET /versao/status` (só perfil `offline`, `VersaoOfflineService`, ADR002).

## domain
**Responsabilidade:** NCM, NBS e aplicabilidade, classificação tributária, tipo de DFe e validação de nomenclatura (`NomenclaturaService`, `ValidacaoNomenclaturaService`) com exceções próprias em `domain/service/exception`.

## config
**Responsabilidade:** `cache` (Caffeine, ADR007), `cors` (ADR012), `security` (stateless, rotas liberadas), `JacksonConfig`.

## shared
**Responsabilidade:** `ArredondamentoUtils` (política numérica única, ADR003), serializers de `BigDecimal` e datas, `ApiExceptionHandler` com `ProblemDetail` (ADR004), `HttpUtils`.

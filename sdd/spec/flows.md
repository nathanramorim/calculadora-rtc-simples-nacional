# Fluxos — calculadora-rtc-simples-nacional

## 1. Cálculo do Simples Nacional (`POST /calculadora/observabilidade/simples-nacional`)
```
Requisição JSON
  ↓ validação na borda
Validação da operação (falha → resposta de erro)
  ↓
Itens em paralelo (threads virtuais, ADR010)
  ↓ por item: nomenclatura (NCM/NBS) → enquadramento → par de alíquotas → CBS e IBS
  ↓ estado CALCULADO, NAO_CALCULADO, erro ou NAO_IMPLEMENTADO (códigos VSN-)
Coleta ordenada por nObj → totalização só sobre itens calculados
  ↓
Resposta com valores por item e totais
```
Arredondamento só por `ArredondamentoUtils` (ADR003). Descrição de um código: `GET /calculadora/observabilidade/simples-nacional/erros?codigo=VSN-001`.

## 2. Atividades do Simples Nacional
```
GET /calculadora/simples-nacional/atividades?data=AAAA-MM-DD (filtros: anexo, tipo de DFe, cClassTrib)
  ↓ AtividadeSimplesService → repositório (SQLite mode=ro)
  ↓ DerivacaoAnexosSimples → ModoFatorR (NAO_APLICAVEL, OPCIONAL, INDISPONIVEL, OBRIGATORIO)
Lista de atividades vigentes
```
`GET /calculadora/simples-nacional/atividades/{codigo}?data=...` consulta uma atividade.

## 3. Versão
`GET /versao`: versão da aplicação, da base e do ambiente.
`GET /versao/status` (perfil `offline`): compara a versão local com a instalação online em `versao.url`; falha na consulta remota devolve campos nulos, sem erro (ADR002). Na subida, a consulta remota é repetida 3 vezes e a aplicação continua se falhar.

## 4. Tratamento de erro
Exceção → `ApiExceptionHandler` → `ProblemDetail` (`type: about:blank` quando o framework não informa). `ErrosCalculoException` devolve a lista `errors` e o `timestamp` (ADR004).

## 5. Banco de dados
Os scripts Flyway ficam no repositório `calculadora-rtc-regime-regular`. Gera-se `./calculadora/db/calculadora-pro.db`, aberto aqui em `mode=ro` (ADR001, ADR009).

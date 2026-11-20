---
description: Como manter qualidade de código Java, higiene de pendências e testes executáveis com Maven.
globs: ["src/main/java/**/*.java", "src/test/**"]
regras: [COD-01, COD-02, COD-04, COD-06, TST-01, TST-02, TST-05]
---

# Guia Prático — Código Limpo e Testes Executáveis

Rotina técnica para `COD-01`, `COD-02`, `COD-04`, `COD-06`, `TST-01`, `TST-02` e `TST-05` (`GOV-04`).

## 1. Código (`COD-01`, `COD-02`, `COD-04`, `COD-06`)
- Identificadores em português sem acento (`calcularAliquota`). JavaDoc obrigatório em domínio, serviços e controllers (`CONTRIBUTING.md`).
- Logs com SLF4J. `System.out` é proibido.
- Erros tratados com exceção de domínio e contexto; o `ApiExceptionHandler` converte em `ProblemDetail` (`COD-03`).
- Remova código morto e comentado na mesma entrega. `TODO` só no formato `TODO(feat-XX): descrição`.
- Verificação: `./mvnw clean test` sem erros ao fim de cada task (`COD-02`).

## 2. Testes (`TST-01`, `TST-02`, `TST-05`)
- Cada critério de aceitação vira teste JUnit. Cubra caminho feliz e violações (JSON inválido, item inexistente, base inconsistente).
- Testes unitários em `testesunitarios/<área>` (incluindo `arquitetura`) e de integração em `testesintegracao/<área>`, com perfil `testes` e o banco gerado. Mudou contrato ou tabela: atualize os testes no mesmo PR (`TST-02`).
- Testes determinísticos, sem depender de relógio nem de banco alterado em runtime (`TST-04`).
- A task só vai a `review_pending` com `./mvnw clean test` em código de saída `0` (`TST-05`).

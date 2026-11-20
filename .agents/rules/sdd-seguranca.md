---
description: Como aplicar validação de entrada, higiene de segredos e logs e governança de dependências no projeto Java.
globs: ["**/*"]
regras: [SEG-01, SEG-02, SEG-04, SEG-05, SEG-07]
---

# Guia Prático — Segurança, Segredos e Dependências

Procedimentos para `SEG-01`, `SEG-02`, `SEG-04`, `SEG-05` e `SEG-07` (`GOV-04`).

## 1. Entrada e escrita (`SEG-01`, `SEG-02`)
- Valide toda entrada na borda com Bean Validation e as regras de nomenclatura. Falha de validação responde por `ProblemDetail`.
- Caminhos e URLs (banco, `versao.url`, `DB_DOWNLOAD_URL`) vêm de configuração, nunca da requisição.
- O nome do banco precisa terminar em `-pro.db` ou `-nonpro.db` (ADR001).
- A aplicação não escreve no banco de referência (`mode=ro`).

## 2. Segredos e logs (`SEG-04`, `SEG-05`)
- Sem credenciais, tokens ou chaves em código, `application*.yml` ou testes. Use variáveis de ambiente e placeholders fictícios.
- Logs e erros não despejam payload fiscal completo, cabeçalhos nem variáveis de ambiente.
- A `WebSecurityConfig` libera todas as rotas (`permitAll`) e o CORS usa só origens configuradas, sem `"*"` (ADR012). Qualquer exposição pública exige revisão e ADR.

## 3. Dependências (`SEG-07`)
- Antes de alterar o `pom.xml`: confirme que JDK ou Spring não atendem; consulte o context7 (se `ativo` em `sdd/memory/mcps.md`) na versão exata.
- Preencha `## Dependências novas` na Spec com artefato, versão, licença e motivo, ou registre `Nenhuma.`.

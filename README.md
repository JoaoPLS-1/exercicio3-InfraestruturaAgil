# Aula 5 — Infraestrutura Ágil

Atividade de checkout, auditoria e linting com GitHub Actions, baseada no site Nova das aulas anteriores.

## Estrutura

- index.html: página inicial existente.
- sobre.html e contato.html: páginas adicionais.
- css/estilo.css: estilos compartilhados.
- .htmlhintrc: regras de validação.
- .github/workflows/ci.yml: CI em push, pull request e execução manual, com ubuntu-latest.
- docs/exercicios.md: respostas e resultados dos experimentos.
- docs/workflow-anterior.yml.txt: cópia da alteração local do workflow anterior.

## Validar localmente

Requer Node.js 22 e npm. Execute:

```sh
npm ci
npm run lint
```

Abra index.html no navegador. A CI primeiro demonstra o workspace sem checkout, depois baixa o código, verifica os três arquivos, conta os HTMLs e executa o HTMLHint com versão exata no package-lock.json. A alternativa CLI prevista no PDF evita depender de uma Action de terceiros.

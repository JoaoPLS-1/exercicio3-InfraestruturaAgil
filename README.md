# Exercício 3 — Infraestrutura Ágil

Site Nova com pacote de distribuição auditado e entrega pelo GitHub Actions.

## Entrega

A esteira `.github/workflows/deploy.yml` valida o HTML, apaga a `dist` antiga, cria uma pasta limpa, copia os HTMLs e `assets/`, lista o pacote e inclui `css/`. A Auditoria de Qualidade usa `test -f` para cada página obrigatória e verifica também a imagem e o CSS. Apenas um pacote aprovado é armazenado como artefato e publicado no GitHub Pages. Se a auditoria falhar, o job de deploy é bloqueado por `needs: build`.

## Executar localmente

Requer Node.js 22 e npm:

```sh
npm ci
npm run lint
```

Abra `index.html` no navegador e navegue pelo menu. O ícone em `assets/nova.svg` é usado no site e acompanha o pacote.

## Experimento de falha

O histórico registrará três fases: entrega inicial com `sobre.html`; renomeação para `quem-somos.html` mantendo a auditoria antiga para provocar falha; e correção da auditoria para obter aprovação novamente. A evidência exigida pelo enunciado será registrada em `docs/evidencias/`, com os links das execuções reais.

Os arquivos anteriores em `docs/` são registros da atividade anterior e não constituem evidência deste exercício.
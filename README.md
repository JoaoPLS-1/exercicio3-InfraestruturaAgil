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

O histórico registra a entrega inicial com `sobre.html`, a renomeação para `quem-somos.html` mantendo a auditoria antiga para provocar falha e a correção da auditoria. O nome final da página é `quem-somos.html`, conforme a Parte 4 do enunciado; todos os menus usam esse nome.

- [Entrega inicial aprovada](https://github.com/JoaoPLS-1/exercicio3-InfraestruturaAgil/actions/runs/39514153210).
- [Falha proposital da auditoria](https://github.com/JoaoPLS-1/exercicio3-InfraestruturaAgil/actions/runs/39514242495): `dist/sobre.html` ausente; deploy ignorado.
- [Print do erro no GitHub Actions](docs/evidencias/falha-auditoria.png), [log original](docs/evidencias/falha-build.log) e [resultado dos jobs](docs/evidencias/falha-jobs.json).
- A correção troca o arquivo esperado por `quem-somos.html`; a execução final será vinculada após confirmação.

Somente o print obrigatório da falha foi capturado. Os logs e metadados foram obtidos da API do GitHub, e a imagem mostra a página real do job com erro.

## Publicação

- [Site no GitHub Pages](https://joaopls-1.github.io/exercicio3-InfraestruturaAgil/).
- [Histórico de execuções](https://github.com/JoaoPLS-1/exercicio3-InfraestruturaAgil/actions).
- O artefato `distribuicao` contém somente os HTMLs, `assets/` e `css/`; arquivos de desenvolvimento e evidências não são publicados no site.

Os arquivos anteriores em `docs/` são registros da atividade anterior e não constituem evidência deste exercício.
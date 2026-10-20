# Respostas e experimentos — Aula 5

## 1. Runner vazio

Em um runner novo, index.html não aparece antes do checkout. O echo imprime qualquer mensagem e retorna sucesso sem verificar arquivos. A CI usa test ! -f index.html antes do checkout e test -f depois para verificar a condição de verdade.

## 2. Checkout e ordem

O checkout baixa o repositório para o workspace. A auditoria anterior não vê o site; a posterior vê os três HTMLs. Os passos compartilham o workspace e executam em ordem. uses executa uma Action, como actions/checkout@v4; run executa comandos no shell, como npm run lint.

## 3. HTMLHint

with fornece entradas para uma Action; por exemplo, node-version e cache no setup-node. Na alternativa do PDF, usamos o HTMLHint via CLI com versão exata, glob **/*.html e regras em .htmlhintrc. Um padrão sem correspondência pode apenas informar que nenhum arquivo foi encontrado, dependendo da ferramenta; por isso a auditoria exige os arquivos esperados. O HTML tem doctype, idioma, título e a regra alt-require habilitada.

## 4. Fail Fast — resultados locais reais

Os defeitos abaixo foram inseridos temporariamente e removidos ap?s cada execução. S?o resultados locais, não logs de execuções remotas. A atividade em dupla depende da participação de um colega.

### Imagem sem alt

Saída: 1; duração local: 138 ms.

```text

   Config loaded: C:\Users\EJJ8NL111\devops-aula2-rpv\DevOps-InfraestruturaAgil\.htmlhintrc

   C:\Users\EJJ8NL111\devops-aula2-rpv\DevOps-InfraestruturaAgil\index.html
      L132 |  <img src="imagem.svg">
                  ^ An alt attribute must be present on <img> elements. (alt-require)

Scanned 3 files, found 1 errors in 1 files (23 ms)

```

### Div sem fechamento

Saída: 1; duração local: 125 ms.

```text

   Config loaded: C:\Users\EJJ8NL111\devops-aula2-rpv\DevOps-InfraestruturaAgil\.htmlhintrc

   C:\Users\EJJ8NL111\devops-aula2-rpv\DevOps-InfraestruturaAgil\index.html
      L132 |  <div>
              ^ Tag must be paired, missing: [ </div> ], start tag match failed [ <div> ] on line 132. (tag-pair)

Scanned 3 files, found 1 errors in 1 files (15 ms)

```

### Ausência de title

Saída: 1; duração local: 117 ms.

```text

   Config loaded: C:\Users\EJJ8NL111\devops-aula2-rpv\DevOps-InfraestruturaAgil\.htmlhintrc

   C:\Users\EJJ8NL111\devops-aula2-rpv\DevOps-InfraestruturaAgil\index.html
      L10 |</head>
           ^ <title> must be present in <head> tag. (title-require)

Scanned 3 files, found 1 errors in 1 files (14 ms)

```

### Desafio: 0 de 3 arquivos corrigidos

```text

   Config loaded: C:\Users\EJJ8NL111\devops-aula2-rpv\DevOps-InfraestruturaAgil\.htmlhintrc

   C:\Users\EJJ8NL111\devops-aula2-rpv\DevOps-InfraestruturaAgil\sobre.html
      L8 |</head>
          ^ <title> must be present in <head> tag. (title-require)

   C:\Users\EJJ8NL111\devops-aula2-rpv\DevOps-InfraestruturaAgil\index.html
      L10 |</head>
           ^ <title> must be present in <head> tag. (title-require)

   C:\Users\EJJ8NL111\devops-aula2-rpv\DevOps-InfraestruturaAgil\contato.html
      L8 |</head>
          ^ <title> must be present in <head> tag. (title-require)

Scanned 3 files, found 3 errors in 3 files (14 ms)

```

### Desafio: 1 de 3 arquivos corrigidos

```text

   Config loaded: C:\Users\EJJ8NL111\devops-aula2-rpv\DevOps-InfraestruturaAgil\.htmlhintrc

   C:\Users\EJJ8NL111\devops-aula2-rpv\DevOps-InfraestruturaAgil\sobre.html
      L8 |</head>
          ^ <title> must be present in <head> tag. (title-require)

   C:\Users\EJJ8NL111\devops-aula2-rpv\DevOps-InfraestruturaAgil\contato.html
      L8 |</head>
          ^ <title> must be present in <head> tag. (title-require)

Scanned 3 files, found 2 errors in 2 files (14 ms)

```

### Desafio: 2 de 3 arquivos corrigidos

```text

   Config loaded: C:\Users\EJJ8NL111\devops-aula2-rpv\DevOps-InfraestruturaAgil\.htmlhintrc

   C:\Users\EJJ8NL111\devops-aula2-rpv\DevOps-InfraestruturaAgil\contato.html
      L8 |</head>
          ^ <title> must be present in <head> tag. (title-require)

Scanned 3 files, found 1 errors in 1 files (16 ms)

```

### Desafio: 3 de 3 arquivos corrigidos

```text

   Config loaded: C:\Users\EJJ8NL111\devops-aula2-rpv\DevOps-InfraestruturaAgil\.htmlhintrc

Scanned 3 files, no errors found (22 ms).

```

Detectar erros na CI reduz o tempo de feedback e evita que problemas conhecidos cheguem ao usuário. Um código de sa?da diferente de zero interrompe os pr?ximos passos do job. Os tempos acima medem apenas o linter local, sem fila, checkout ou instala??o da CI.

## 5. Versionamento de Actions (5 linhas)

1. Uma referência inexistente como checkout@v99 impede a resolução da Action antes da validação do site.
2. Usar uma referência móvel sem controle pode trazer mudan?as incompat?veis do autor.
3. Fixar uma versão principal limita mudan?as incompat?veis, mas a tag ainda pode mudar.
4. Um SHA completo oferece uma referência mais precisa e protege contra alteração da tag.
5. Atualiza??es revisadas equilibram correções de segurança e estabilidade; mantivemos checkout@v4 como no roteiro.

O teste remoto com @v99 não foi realizado: a versão final mant?m uma referência funcional. A CI publicada demonstra o estado antes/depois do checkout; não representa pushes separados de cada etapa do laborat?rio.

## 6. Regras e vêrios arquivos

O desafio acima mostra três erros simult?neos e a correção de um arquivo por vez. As regras cobrem nomes e atributos minúsculos, aspas duplas, doctype inicial, título, alt, pares de tags, IDs ?nicos e atributos sem duplica??o. O CSS compartilhado mant?m a aparência do site original.

<img src="https://avatars1.githubusercontent.com/u/3846050?v=4&s=200" width="127px" height="127px" align="left"/>

# Git Style Guide

Style Guide para o Git sugerido pela Pagar.me

<br>

## Branches

- [1.1](#) Escolha nomes curtos e descritivos.

  > Identificadores correspondentes a tickets em um serviço externo (ex: issue no github) são uma boa forma de dar nome as branchs.

  ```sh
  # bom
  $ git checkout -b feature/oauth

  # bom: usando identificadores
  $ git checkout -b fix/issue-15

  # ruim: muito vago
  $ git checkout -b login_fix
  ```

- [1.2](#) Use traços para separar palavras.

  ```sh
  # bom
  $ git checkout -b feature/add-webhook

  # ruim
  $ git checkout -b feature/add_webhook
  ```

## Commits

- [2.0.1](#) (Dica bônus) Busque deixar as mensagens em inglês!

  > Inglês é uma lingua universal e pode facilitar a sua comunicação com outros desenvolvedores!

- [2.1](#) Cada commit deve representar uma única mudança.

  > Não faça várias mudanças em um só commit. Por exemplo, se um patch corrige um bug e otimiza a performance de uma feature, divida isso em dois commits separados.

  > **Dica:** Use git add -p para adicionar interativamente porções especificas dos arquivos modificados.

- [2.2](#) Não divida uma única mudança em vários commits.

  > Por exemplo, a implementação de uma feature e de seus testes devem estar no mesmo commit.

- [2.3](#) Faça commits cedo e com frequência.

  > Commits pequenos e independentes são mais fáceis de entender e reverter quando algo da errado.

  > **Dica:** Use git add -p para adicionar interativamente porções especificas dos arquivos modificados.

* [2.4](#) Commits devem ser ordenados de forma lógica.

  > Se o commit X depende de mudanças feitas no commit Y, então o commit Y deve vir antes do commit X. De forma similar, se o commit A resolve um bug do commit B, isso deve estar incluido na mensagem do commit A

- [2.5](#) NUNCA deixe um commit quebrar uma funciolidade que esteja funcionando.

  > SEMPRE garanta que a branch master apenas contenha commits que são 100% funcionais, e tenham seus próprios testes e correções.

  > **Nota:** Quando estiver trabalhando sozinho em uma branch local que ainda não foi "pushada", é tranquilo usar commits como snapshots temporários do seu trabalho. Entretanto, você ainda deve aplicar tudo do que foi dito acima quando pushar para para o repositório remoto. Para faze-lo, é importante entender `git rebase -i`.

## Mensagens

- [3.1](#) Use o editor ao invés do terminal, quando estiver escrevendo uma mensagem de commit.

  > **Por que?** Fazer commits pelo terminal te encoraja a escrever tudo em uma só linha, que resulta em uma mensagem nada informativa e ambigua.

  ```sh
  # bom
  $ git commit

  # ruim: sem mensagens de commit
  $ git commit -m "Quick fix"
  ```

- [3.2](#) Uma mensagem de commit consiste de 3 partes distintas separadas por uma linha em branco. O título, um corpo e um rodapé opcional. O layout fica algo como:

  ```
  context: assunto

  corpo

  rodapé
  ```

  - **Titulo:** Consiste no contexto e no assunto da mensagem.
  - **Contexto:** a parte da aplicação que está sendo alterada.
  - **Subject:** o que está sendo alterado. Os assuntos não devem ser maiores que 50 caracteres, devem começar com letras minúsculas, e não terminar com 'periodos'. Use um tom imperativo para descrever o que o commit faz, invés de descrever o que ele fez. Por exemplo: Use `change`, invés de `changed` ou `changes`.
  - **Corpo:** Use o corpo para explicar o "o que" e "por que" de um commit, e não "como". Quando estiver escrevendo um corpo (body), a linha em branco entre o titulo e o corpo é necessária e você deve limitar o tamanho de cada linha para não mais de 72 caracteres. Quando estiver escrevendo uma mensagem, pense no que seria útil caso você o acesse daqui um ano.
  - **Rodapé (footer):** O footer é opcional, e é usado para referencias IDs de issues, etc.

  Commit de exemplo:

  ```
  core: Resuma as mudanças em 50 caracteres ou menos.

  Text explicativo, se necessário. Mantenha-o com mais ou menos 72
  caracteres. Em alguns contextos, a primeira linha pode conter o
  assunto do commit e o resto do texto, o corpo do commit. A linha em
  branco separando o assunto do corpo é necessária (a não ser que você
  omita o corpo inteiro); várias ferramentas como `log`, `shortlog` e
  `rebase` podem se confundir se você rodar os dois ao mesmo tempo.

  Explique o problema que o commit está resolvendo. Foque no por que
  de você estar fazendo aquela mudança ao invés de como (o código irá
  explicar isso). Há efeitos colaterais ou consequências não intuitivas
  nessa mudança? Aqui você explica isso.

  Paragrafos adicionais vem depois das linhas em branco.

   - "Bullet points" são permitidos

   - Tipicamente um hifen ou asterisco é usado para as "bullets", precedidos
   por um espaço em branco, com linhas em branco entre eles, mas as convenções
   variam bastante aqui.

  Se você usa um rastreador de issues, coloque as referencias no fim do commit:

  Resolve: #123
  Veja também: #456, #789
  ```

## Merging

- [4.1](#) Não reescreva históricos já publicados.

  > **Por que?** O histórico do repositório é valioso da sua forma e é muito importante ser capaz de dizer o que realmente aconteceu.

  Alterar históricos que já foram publicados é uma fonte de problemas para qualquer um que trabalhe no projeto. Entretanto, há casos em que fazer isso é permitido. Por exemplo:

  - Você é o único trabalhando trabalhando na branch e não está sendo revisado.
  - Você quer limpar sua branch ou fazer um rebase para a "master" para poder fazer um merge depois.

- [4.2](#) Mantenha o histórico limpo e simples.

  > Tenha certeza que isso concorde com o style guide e faça qualquer ação necessária caso não concorde (reescrever mensagens, reordenar commits etc.).

- [4.3](#) Rabases na branch também sofrerão merge

  > **Nota:** Esta estratégia funciona melhor em projetos com branches que duram pouco tempo. Em outros casos, pode ser melhor fazer um merge na branch master ao invés de fazer o rebase na mesma.

- [4.4](#) NUNCA commite algo como "Fix linter" ou "Fix tests".

  > **Por que?** Essas "correções" podem ser feitas junto com o commit que as originaram.

- [4.5](#) NUNCA junte todos commits de uma branch antes de fazer um merge.

- [4.6](#) NUNCA use git merge master em uma branch.

  > SEMPRE use git rebase master, depois force-push, espere até a CI ficar limpa e então faça um merge na master.

## Precisa de ajuda?

Se você não está familiarizado com os comandos do git ou precisa de ajuda para alcançar o style guide, confira [k88hudson/git-flight-rules](https://github.com/k88hudson/git-flight-rules) para algumas dicas de uso e passo-a-passo (inglês).

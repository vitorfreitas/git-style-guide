# git-style-guide

Git styleguide followed by us here at Pagar.me

## Guidelines

### Branches

* Nomes de branches devem ser pequenos e descritivos. E.g. `oauth-migration` é um nome bom por ser curto e conter a essência do que está sendo feito. `validation-fix` é ruim porque é curto e vago. `bulk-anticipation-d0-api-admin-fix` é ruim porque é longo, e poderia ser resumido para `d0-anticipation`. **Uma coisa que acho importante complementar: na dúvida entre sucinto e não-descritivo e longo e descritivo, escolher longo e descritivo.**

* Devemos deletar branches dos repositórios quando elas tiverem sido mergeadas por padrão.

* Devemos separar palavras de branches com `-` e não com `_` ou qualquer coisa. Isso é uma questão de estilo.

* Quando duas pessoas estiverem trabalhando em uma feature, ter `bob/XXX` e `gui/XXX` pra sinalizar que são duas pessoas trabalhando na mesma coisa. Não devemos usar `XXX1` e `XXX2` pra isso. Sempre colocar o autor antes de uma `/`.

* Usar prefixos de branch como padrão para denotar o que ela faz, sendo separados por uma `/`. Prefixos válidos (evitar prefixos alheios a estes):
    * `fix`: conserta algo que deu errado
    * `task`: faz ajustes ao código, como refactors
    * `feature`: adiciona uma feature nova

**Exemplos de branch**: `feature/d0-anticipation`; `bob/fix/antifraud-metadata-esindex`; `task/lint-on-ci`.

Em suma, acho que já temos todas essas coisas de mexer com branches enraizados na Pagar.me exceto o primeiro item (acho que muitos, inclusive eu, fazemos uns nomes de branches bem merda). Acho que o importante aqui é menos esforço pra mudar e mais atenção nas boas práticas do que já fazemos.

### Commits

**DICA**: Pessoal, aprendam a usar o `git rebase -i`. É uma das features mais úteis pra limpar, editar, reescrever, squashear e tudo mais os seus commits. Aprender a usar isso é provavelmente o melhor jeito de conseguir efetivamente seguir essas guidelines. Ninguém espera que os commits já saiam bonitinhos assim do programador – pelo contrário! Vai sair muito "WIP", "fix wtf", "i dont know what im doing haha". Aí temos que pegar commits e ir editando, reescrevendo etc. até ficar tudo bonito para o push. Do contrário, vamos acabar só pensando "Não vale a pena o esforço pra seguir as guidelines, vou shipar a feature e ignorá-las."

* Todos os commits devem ser em inglês. Pode parecer pedantismo, mas acho que vale sim a pena corrigir coisas de gramática ou palavras que não existem em inglês no review, porque é importante que nós consigamos nos entender depois com facilidade.

* Cada commit deve ser uma mudança lógica simples. Não faça várias mudanças lógicas em um commit. Por exemplo, se uma alteração corrige um bug e otimiza a performance de uma funcionalidade, o divida em dois commits separados. Fazer essa divisão é sempre um problema em aberto, então na dúvida, acho que a melhor coisa é perguntar a opinião de outros devs ou do reviewer de como eles dividiriam! (Dica: use `git add -p` pra criar commits em pequenos blocos).

* Commits devem ser ordenados logicamente. Por exemplo, se commit X depende de uma mudança feita no commit Y, então commit Y deve vir antes do commit X.

* `git commit -m` deve ser proibido. Façam só `git commit`! Commits são mil vezes melhor feitos quando são editados com um **editor** (não precisa ser o `vim` pra quem não sabe -- tem aí o `nano`, que é super simples e faz esse trabalho).

#### Mensagens

Essa parte é polêmica e muitas das convenções que eu estou citando aqui não têm nenhuma vantagem em particular exceto darem uniformidade (algo como o StandardJS: o valor não está naquele estilo, mas no fato de que todo mundo usa aquele estilo). Dito isso, boa parte delas saiu de projetos como o Linux e o Git (que conseguem ter **muitos** contribuidores e dão certo), então é o mais perto de um "standard de Git messages" que temos.

* A primeira linha do commit é o seu **título** e deveria ter até 50 caracteres (o `vim`, quando edita commits, é super legal pra te avisar essas coisas). Embora devamos tentar ter no máximo 50chars, é aceitável, como exceção, títulos de até 72 chars. Uma boa convenção é **citar a parte da codebase que você está mudando** e resumir o que foi feito. Títulos de commits devem começar com **verbos no imperativo** (finja que você está mandando a sua codebase fazer alguma coisa!) e **não deveriam ter pontuação* (porque é um título). Por exemplo: `bulk-anticipation: enable D+0 anticipations`; `hal: refactor subscription fee calculation`. ERRADO: `hal: fixed subscription fees` (não está no imperativo!); `change hal subscription fees` (fugiu do padrão de começar commits com a parte sendo mudada).

* Caso seja difícil encontrar a coisa pra vir antes dos dois pontos (por exemplo, muitas partes do código sendo mudadas), é aceitável, nesses casos, não colocar um prefixo. Exemplo: `Apply StandardJS coding style` (isso se aplica ao projeto todo). Mas nota: esses casos deveriam ser exceção, não a regra!

* Aí o resto da mensagem de commit deve ser composta de linhas de até 72 caracteres (o `vim`, mais uma vez, lida com isso automaticamente. Imagino que configurar o `nano` pra fazer isso deve ser fácil também, e vale o esforço!). Aqui você deve falar também no estilo **imperativo**, como se você estivesse dando ordens pra codebase (não dizer "This commit allows us to perform this", e sim "Allow us to perform this").

* IMPORTANTE: Ter mensagens de commit fora o título deve ser o **padrão**. Commits que só têm o título devem ser considerados exceções.

* O ponto dessa mensagem é realmente explicar o que o commit faz, e não tem muitas regras fora o estilo imperativo. Assim como a gente explica coisas com detalhe nos PRs temos que começar a fazer o mesmo com commits. O ideal é que commits **expliquem qual era o problema que a implementação buscava resolver em detalhe**, **fale por que determinadas decisões técnicas foram feitas**, entre outras informações relevantes para entender por que o código que foi escrito foi feito. Uma coisa importante é evitar explicar o que o código faz em um commit -- o código deveria explicar isso sozinho (clean code! :D). Quando for necessário, façam referências a commits passados que possam ter a ver com a implementação; ou links que possam ter servido de inspiração etc. etc. Mais uma vez, devemos fazer isso **em inglês**. Os melhores lugares pra aprender com bons commits são provavelmente os repositórios do git e do Linux (o Linus Torvalds tem orgulho do alto padrão e do bom gosto que ele tem pra commits bem feitos).

* Explicar, sempre, todas as ações feitas por um commit. No caso de um commit que mexeu no controller de transactions pra mexer num bug e aproveitou pra fazer um refactor, não tenham medo de colocar:

```
Fix bug ......

Refactor ...... to add more clarity.

Improve testes for ....... for this case.
```

* **Nenhum commit deveria ser quebrado**. Por exemplo, eu *nunca* deveria mudar o transaction helper em um commit de forma que quebre o transaction controller e só mudar o transaction controller  pra consertar isso em outro commit.

Essa propriedade de "todos os commits funcionarem" às vezes pode inflar alguns commits (por isso que é bom ter mensagens boas), mas permite outras coisas muito boas, como poder saber exatamente **qual commit quebrou alguma coisa** (i.e., não passou nos testes). Podemos também tracear bugs com `git bisect`: (https://git-scm.com/docs/git-bisect) nos commits novos que seguirem esse estilo. Outra coisa: impede commits que tenham no seu corpo nada exceto "Fix API to conform to 61a52ef."

* **Importante**: pra vocês não dizerem que git style guide é só coisa de frescura, segue um exemplo de como um Git style guide pode melhorar nosso monitoramento. Deveríamos sempre **testar ou antes de ou junto com um commit que muda uma feature**.
    * Exemplo 1: se tem uma feature mal testada na qual vamos mexer, devemos **primeiro testar o behavior atual dela e depois fazer changes**, pra garantir que nossas changes não vão quebrar nada.
    * Exemplo 2: adicionamos uma feature e queremos testá-la. Devemos adicionar os testes no *mesmo commit*, pra podermos encontrar bugs na menor unidade possível de controle de versionamento.
    * Exemplo 3: temos um bug conhecido e queremos consertá-lo. Em alguns casos faz sentido testar o behavior bugado antigo nos nossos testes em um commit pré-fix, e testar o behavior certo no commit pós-fix. Isso vai fazer a gente testar **cientificamente** os nossos fixes e acabar com o nosso canary de pobre de "ver se funciona em uma máquina com fix deployado e quebra em outra sem fix deployado".

* A partir disso, não precisaremos mais escrever descrições elaboradas pra pull requests como fazemos hoje, porque tudo isso já vai estar feito, e com muito mais detalhe, nos próprios commits de forma muito mais fácil de browsear (dá pra dar um `git blame` fácil, mas um `git pull-request-blame` não existe).

### Merging

* Continuar fazendo o que fazemos: a `master` nunca pode ser reescrita; branches individuais podem ter `git push -f` pra "consertar" um histórico temporário de desenvolvimento.

* **NUNCA** deve haver um commit como "Fix linter" ou "Fix tests". Todas essas coisas devem ser squasheadas nos commits que fizeram a change. Isso é uma consequência natural das regras de commits citadas anteriormente, mas vale reiterar.

* **NUNCA** squashear completamente uma branch antes de mergeála, a não ser que de fato ela consista de somente um commit lógico.

* **NUNCA** dar `git merge master` em uma branch. Sempre dar `git rebase master`, dar force-push, esperar o CI passar pra então mergear na master.

* Por convenção, devemos mergear na `master` pelo GitHub e não pelo Git direto (i.e. `git checkout master; git merge --no-ff branch; git push`). É o que já fazemos, e evita confusões como esquecer de especificar que devemos fazer sempre um non-fast-forward merge.

### Pull Requests

* Como falei anteriormente, pull requests devem estar lá para documentar merges mas não para fazer o que temos hoje e explicar o que deveria ser explicado em commits individuais. A descrição do PR deve ser **somente** um sumário do que todos os seus commits juntos fazem (meio que uma "cover letter" da sua branch).

* Não deve haver pull request WIP. WIP deve ser feito em branch sem PR aberto. Todos os pull requests devem estar waiting for review.

## Misc

Um tempo atrás eu e o Thales aproveitamos um negócio do Google chamado `git-hyper-blame` que dado um conjunto de commits, ignora eles na hora de gerar o blame. Isso é útil pra tirar do blame os commits de aplicar o StandardJS e conseguirmos ver qual foi o commit do Jojo em 2014 que pode explicar minimamente o sentido de algo em que estamos mexendo. Outro caso bom pra remover são os commits de ajuste pros projetos passarem no linter. Acho que seria legal todo mundo ter isso pra conseguir se aproveitar o máximo possível do `blame`.

## Conclusão

Provavelmente vai ter muitas mudanças em como fazemos as coisas com o Git dado um style guide (que não precisa ser esse, ainda deve ter discussão sobre quais devem ser os standards). Mas o ponto é: deveríamos ter um style guide e segui-lo, senão vamos nos perder completamente com o número elevado de devs.

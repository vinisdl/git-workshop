O que é Git?
============

Git é um sistema de **controle de versão** *distribuído* [1]

[1] <a href="http://git-scm.com/about">http://git-scm.com/about</a>

Obtendo o Git
--------------

Um pouco de limpeza aqui. Presumimos, é claro, que você tem o Git instalado,
(esperançosamente \>= 1.7.0).

Se não o tiver, você pode instalá-lo a partir dos downloads na página inicial do Git ou pode
instalar a [interface gráfica do Git do Github](https://help.github.com/articles/set-up-git/).

Configuração
------------

A primeira coisa a fazer é configurar sua identidade. Isso o identifica para
outras pessoas que baixam o projeto.

    $ git config --global user.name "Seu Nome"
    $ git config --global user.email seu.email@example.com

Como um passo útil, você pode querer configurar o Git para usar seu editor favorito

    $ git config --global core.editor emacs

Começando sua jornada
----------------------

Primeiro, clone este repositório:

    $ git clone https://github.com/kuahyeow/git-workshop.git

Você pode querer fazer um fork (criar sua própria cópia) do projeto no GitHub e
clonar a partir do seu próprio repositório. Você pode encontrar o botão de fork no canto superior direito da
tela em um repositório do GitHub, ou obter mais ajuda sobre isso [aqui](https://help.github.com/articles/fork-a-repo/).

Depois de clonar seu repositório, você deve ver um diretório chamado `git-workshop`. Este é o seu `diretório de trabalho`

    $ cd git-workshop
    $ ls


Para os curiosos, você também deve ver o subdiretório `.git`. É aqui que
todos os dados e o histórico do seu repositório são mantidos.

    $ ls .git

Você verá:

    Mode                 LastWriteTime         Length Name                                                                                 
    ----                 -------------         ------ ----
    d-----         8/26/2024   4:54 PM                hooks
    d-----         8/26/2024   4:54 PM                info
    d-----         8/26/2024   4:54 PM                objects
    d-----         8/26/2024   4:54 PM                refs
    -a----         8/26/2024   4:54 PM            130 config
    -a----         8/26/2024   4:54 PM             73 description
    -a----         8/26/2024   4:54 PM             23 HEAD

A área de preparação
-------------------

Agora, vamos tentar adicionar alguns arquivos ao projeto. Crie alguns
arquivos.

Vamos criar dois arquivos chamados `bob.txt` e `alice.txt`.

    $ touch alice.txt bob.txt

Vamos usar uma analogia com o correio.

No Git, você primeiro adiciona conteúdo à `área de preparação` usando `git add`.
Isso é como colocar as coisas que você quer enviar em uma caixa de papelão.
Você finaliza o processo e o registra no índice do git usando
`git commit`. Isso é como selar a caixa - agora está pronta para enviar.

Vamos adicionar os arquivos à área de preparação

    $ git add alice.txt bob.txt

Comitando
----------

Você está agora pronto para fazer o commit. A flag `-m` permite que você insira uma mensagem
para acompanhar o commit ao mesmo tempo.

    $ git commit -m "Estou adicionando dois novos arquivos"

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Com dificuldades? Peça ajuda à equipe do workshop

Vamos ver o que aconteceu
--------------------------

Agora devemos ter um novo commit. Para ver todos os commits até agora, use
`git log`

    $ git log

O log deve mostrar todos os commits listados do mais recente para o menos
recente. Você verá várias informações, como o nome do autor,
a data em que foi comitado, um número SHA do commit e a mensagem para o
commit.

Você também deve ver seu commit mais recente, onde você adicionou os dois novos
arquivos na seção anterior. No entanto, o git log não mostra os arquivos
envolvidos em cada commit. Para ver mais informações sobre um commit, use
`git show`.

    $ git show

Você deve ver algo semelhante a:

    commit 5a1fad96c8584b2c194c229de7e112e4c84e5089
    Author: kuahyeow 
    Date:   Sun Jul 17 19:13:42 2011 +1200

        Estou adicionando dois novos arquivos

    diff --git a/alice.txt b/alice.txt
    new file mode 100644
    index 0000000..e69de29
    diff --git a/bob.txt b/bob.txt
    new file mode 100644
    index 0000000..e69de29

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Com dificuldades? Peça ajuda à equipe do workshop

Uma digressão necessária
------------------------

Nesta seção, vamos adicionar mais mudanças e tentar recuperar
de erros.

Este próximo passo vai ser difícil. Precisamos adicionar
algum conteúdo ao `alice.txt`.

Abra `alice.txt` e digite sua linha favorita de uma música, ou:

e.g. Lorem ipsum Sed ut perspiciatis, unde omnis iste natus error sit
voluptatem accusantium doloremque laudantium

Então **salve** o arquivo

O que mudamos? Um comando muito útil é `git diff`. Isso é muito
útil para ver exatamente o que você alterou.

    $ git diff

Você deve ver algo como o seguinte:

    diff --git a/alice.txt b/alice.txt
    index e69de29..2aedcab 100644
    --- a/alice.txt
    +++ b/alice.txt
    @@ -0,0 +1 @@
    +Lorem ipsum Sed ut perspiciatis, unde omnis iste natus error sit voluptatem accusantium doloremque laudantium

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Com dificuldades? Peça ajuda à equipe do workshop

Área de preparação novamente
----------------------------

Agora vamos adicionar o nosso arquivo modificado, `alice.txt`, à área de preparação. Você
lembra como fazer isso?

Em seguida, verifique o `status` de `alice.txt`. Está na área de preparação agora?

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Com dificuldades? Peça ajuda à equipe do workshop

Desfazendo
----------

Vamos supor que não gostamos de ter colocado Lorem ipsum em `alice.txt`. Uma
vantagem da área de preparação é que ela permite que possamos voltar atrás antes de
fazer o commit - o que é um pouco mais difícil de voltar depois. Lembrando a analogia do correio - é mais fácil tirar o correio da caixa de papelão antes de selá-la do que depois.

Aqui está como voltar da área de preparação:

    $ git reset HEAD alice.txt

    Unstaged changes after reset:
    M   alice.txt

Compare o `git status` agora com o git status da seção anterior. Como isso difere?

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Com dificuldades? Peça ajuda à equipe do workshop

Sua área de preparação agora deve estar vazia. O que aconteceu com as mudanças de Lorem
Ipsum? Elas ainda estão lá. Estamos agora de volta ao estado justo antes de
adicionarmos este arquivo à área de preparação. Voltando à analogia do correio, acabamos de tirar nossa carta da caixa.

Desfazendo II
-------------

Às vezes, não gostamos do que fizemos e desejamos voltar ao último estado *registrado*. Neste caso, desejamos voltar ao estado
justo antes de adicionar o texto Lorem ipsum a `alice.txt`.

Para conseguir isso, usamos `git checkout`, assim:

    $ git checkout alice.txt

Você agora desfez suas mudanças. Seu arquivo agora está vazio.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Com dificuldades? Peça ajuda à equipe do workshop

Branching
---------

A maioria dos grandes códigos tem pelo menos dois branches - um branch 'live' e um branch 'development'. O branch live é o código que está pronto para ser implantado em um site ou baixado pelos clientes. O branch de desenvolvimento permite que os desenvolvedores trabalhem em recursos que podem não estar livres de bugs. Somente quando todos estão satisfeitos com o branch de desenvolvimento ele é mesclado com o branch live.

Criar um branch no Git é fácil. O comando `git branch`, quando usado sozinho, lista os branches que você tem atualmente

    $ git branch

O `*` deve indicar o branch atual em que você está, que é `master`.

Se você deseja iniciar outro branch, use
`git checkout -b (novo-nome-do-branch)` :

    $ git checkout -b exp1

Tente git branch novamente para verificar em qual branch você está atualmente:

    $ git branch
      exp1
    * master

O novo branch está agora criado. Agora vamos trabalhar nesse branch. Para alternar
para o novo branch:

    $ git checkout exp1

`git checkout (nome-do-branch)` é usado para trocar de branches.

Vamos realizar alguns commits agora,

    $ echo 'some content' > test.txt
    $ git add test.txt
    $ git commit -m "Adicionado txt experimental"

Agora, vamos compará-los com a branch master. Use `git diff`:

    $ git diff master

Basicamente, o que a saída acima indica é que `test.txt` está presente na branch `exp1`, mas está ausente na branch `master`.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Está com dificuldade? Peça ajuda à equipe do workshop

Agora você me vê, agora você não me vê
---------------------------------------

O Git é eficiente o suficiente para gerenciar seus arquivos quando você alterna entre branches. Volte para a branch master.

Tente alternar de volta para a branch master (Dica: É o mesmo comando que usamos para alternar para a branch exp1 acima).

Agora, onde está nosso arquivo `test.txt`?

    $ ls
    README.textile  alice.txt   bob.txt     gamow.txt

Como você pode ver, o novo arquivo que você criou na outra branch desapareceu. Não se preocupe, ele está guardado com segurança e reaparecerá quando você voltar para essa branch.

Agora, volte para a branch `exp1` e verifique se o `test.txt` está agora presente.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Está com dificuldade? Peça ajuda à equipe do workshop

Mesclagem
---------

Agora vamos tentar a mesclagem. Eventualmente, você vai querer mesclar duas branches após a conclusão do trabalho. `git merge` permite fazer isso.

A mesclagem no Git funciona primeiro alternando para a branch na qual você deseja *mesclar*, e depois executando o comando para mesclar a outra branch.

Agora queremos mesclar nossa branch `exp1` na `master`. Primeiro, mude para a branch master:

    git checkout master

Em seguida, mescle a branch `exp1` na `master`:

    $ git merge exp1

Você vê a seguinte saída?

    Merge made by recursive.
     test.txt |    1 +
     1 files changed, 1 insertions(+), 0 deletions(-)
     create mode 100644 test.txt

Você deve estar na branch para a qual deseja mesclar e, em seguida, sempre especificar a branch que deseja mesclar.

Neste ponto, você também pode usar `gitk` para visualizar as alterações e como as duas branches foram mescladas.

Conflitos de Mesclagem
----------------------

O Git é bastante bom em mesclar automaticamente, mesmo quando o mesmo arquivo é editado. No entanto, existem algumas situações em que a mesma linha de código é editada de maneira que o computador não consegue determinar como mesclar. Isso resultará em um conflito que você terá que resolver.

Agora, vamos praticar a resolução de conflitos de mesclagem. Lembre-se de que os conflitos são causados por mesclagens que afetam o mesmo bloco de código.

Aqui está uma branch que preparei anteriormente. A branch é chamada `alpher`. Execute o código abaixo para configurá-la (não se preocupe se não entender):

    $ git checkout alpher

Você deve agora ter uma nova branch chamada `alpher`. Tente mesclar essa branch na `master` agora e resolva o conflito resultante.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Está com dificuldade? Peça ajuda à equipe do workshop

Resolvendo um Conflito
----------------------

Você deve ver um conflito com o arquivo `gamow.txt`. Isso significa que a mesma linha de texto foi editada e comitada tanto na branch `master` quanto na branch `alpher`. A saída abaixo basicamente mostra a situação atual:

    Auto-merging gamow.txt
    CONFLICT (content): Merge conflict in gamow.txt
    Automatic merge failed; fix conflicts and then commit the result.

Se você abrir o arquivo `gamow.txt`, verá algo semelhante a:

    $ cat gamow.txt
    <<<<<<< HEAD
    It was eventually recognized that most of the heavy elements observed in the present universe are the result of stellar nucleosynthesis (http://en.wikipedia.org/wiki/Stellar_nucleosynthesis) in stars, a theory largely developed by Bethe.
    =======

    http://en.wikipedia.org/wiki/Stellar_nucleosynthesis
    Stellar nucleosynthesis is the collective term for the nuclear reactions taking place in stars to build the nuclei of the elements heavier than hydrogen. Some small quantity of these reactions also occur on the stellar surface under various circumstances. For the creation of elements during the explosion of a star, the term supernova nucleosynthesis is used.
    >>>>>>> alpher

O Git usa marcadores de resolução de conflitos padrão. A parte superior do bloco, que é tudo entre `<<<<<< HEAD` e `======`, é o que estava na sua branch atual.\
A parte inferior é a versão presente na branch `alpher`. Para resolver o conflito, você deve escolher um dos lados ou mesclar os dois conforme achar melhor.

Por exemplo, eu posso decidir escolher a versão da branch `alpher`.

Agora, tente **resolver o conflito de mesclagem**. Escolha o texto que você acha melhor (peça ajuda se ficar com dúvida).

Depois de fazer isso, você pode marcar o conflito como resolvido usando `git add` e `git commit`.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Está com dificuldade? Peça ajuda à equipe do workshop

    $ git add gamow.txt
    $ git commit -m "Conflito resolvido"

Parabéns. Você resolveu o conflito. Tudo está bem no mundo.

Fim
---

Você aprendeu:

1. Clonar um repositório
2. Comitar arquivos
3. Verificar o status
4. Verificar diferenças
5. Desfazer alterações
6. Criar branches e mesclar
7. Resolver conflitos

Agora você pode escolher dois caminhos: Parte II (abaixo), que cobre viagens no tempo e manipulação do histórico do Git, ou Parte III (ainda mais abaixo), que cobre pull requests do GitHub e gifs de gatos.

Parte II
========

Confira a branch `revert` neste repositório para mais instruções! Você sempre pode voltar a esta versão do README verificando a branch master.

Parte III
=========

GitHub
------

Mas, espere. Há mais. E quanto a esse compartilhamento distribuído com o Git?

Para compartilhar, precisaremos de um servidor para hospedar nossos repositórios Git. O GitHub (<a href="https://github.com/">github.com</a>) é provavelmente o lugar mais fácil para começar.

Faça login ou registre-se no GitHub
------------------------------------

Se você já tem uma conta, pode pular para a criação do repositório no GitHub ou para forkar este repositório e cloná-lo para sua máquina local.

Caso contrário...

Vá para <a href="https://github.com/signup">criar uma conta</a> no GitHub; ou faça login em sua conta do GitHub se você já tiver se registrado anteriormente.

Dica: Pode ser necessário configurar o cache do Git para sua senha do GitHub - veja <a href="https://help.github.com/articles/set-up-git">aqui</a>.

Depois volte aqui, nós esperamos.

Crie seu primeiro repositório no GitHub
--------------------------------------

Um repositório (repo) é um local onde você armazena seu código. Você estava praticando no seu próprio repositório agora mesmo na Parte 1!

O seguinte <a href="https://help.github.com/articles/create-a-repo">tutorial</a> mostrará como criar um repositório no GitHub - que você pode então compartilhar com outros.

Depois volte aqui, nós esperamos.

Fork de um repositório
----------------------

Vá para [este tutorial](https://help.github.com/articles/fork-a-repo).

Depois volte aqui, nós esperamos.

Vamos colaborar!
----------------

Confira a branch `pull_request` neste repositório para mais instruções! Você sempre pode voltar a esta versão do README verificando a branch master.

Fim
---

Você aprendeu:

1. Fork de um repositório no GitHub
2. Git push
3. Git pull

### Referências e Leitura Adicional

Recomendo fortemente estes recursos para continuar sua prática com o Git:

- <a href="http://try.github.com">http://try.github.com</a> Outro tutorial para iniciantes em Git
- <a href="http://git-scm.com">http://git-scm.com</a> Site oficial, com ajuda muito útil, livro e vídeos
- <a href="http://gitref.org">http://gitref.org</a>
- <a href="http://www.kernel.org/pub/software/scm/git/docs/everyday.html">http://www.kernel.org/pub/software/scm/git/docs/everyday.html</a>

Autor
------

Este trabalho está licenciado sob a Licença Creative Commons
Atribuição-NãoComercial-CompartilhaIgual 3.0\
<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">http://creativecommons.org/licenses/by-nc-sa/3.0/</a>\
Autor: Thong Kuah\
Contribuintes: Andy Newport, Nick Malcolm
# projeto-chale

txt pelo git

git init é dado uma única vez e é dado para tornar um "arquivo" git

stash
Usado para deixar uma alteração em standby, qdo ainda não deve ser commitada

stash pop
Busca a alteração stash que está em standby

# Revertendo Commit
1 - Com -> git revert (melhor opção para usar no master)
reverter um commit urgente

Mas atenção: antes de dar o git revert (reverter commit), é necessário dar git log - comando para ver commits lançados - para ver qual qual o commit que será revertido. 
Então seguindo a lógica:
1º git log - para ver os commits já lançados
2º git revert - depois de ver os commits que foram lançados qual será revertido 

2 - Com -> Reset (melhor opção para usar em branch fora do master)

git reset --hard <numero da hash>
Volta para o commit tal e ignora -apaga- todos os commits após este

git reset --soft <numero da hash>
Volta para o commit tal e todos os commits q fora mudados após este voltam para a área de standing

# Como editar o título do último commit ? (antes do push)
git commit --amend ...
Daí só mudar o título do commit

# Como editar o último commit ? (antes do push)
git commit -ammed
No final da vi usamos o comando (:wd) 

Fazemos a alteração necessária no arquivo daí
git add <nome do arquivo>
git commit --amend 

# Como sei que foi anexado a mudança ?
git log - para ver o hash do commit
git show <hash do commit> para mostrar a alteração 

# Como pegar um commit específico de um branch e por no meu ?
git cherry-pick <hash>
    O git cherry-pick <hash> pega um commit de uma determinada branch e copia para a branch que eu quiser add o commit. Essa cópia de commit vai trazer copiar tudo, mas caso exista algum conflito em alguma linha, eu tenho de resolver.
    Git cherry-pick <hash> é interessante pq não precisa usar merge, ela faz a mesma coisa sem alterar o histórico. 

Ex.:
git checkout - <nome da branch>
git log (para ver os hash dos commits)
    seleciona a hash desejada
git cherry-pick <hash>

# Commitar trecho específico
git add -p

    Mesmo que seja no mesmo arquivo é possível fazer commits separados.

Ex.:
Em um arquivo tal faço 1 alteração salvo, depois faço mais uma alteração e salvo de novo. Para fazer um commit para cada alteração faço:
-->git add -p 
Vai dar o commit 1.
Vai entrar na tela de separação de alterações. Irão aparecer as alterações separadamente. Primeiro vai aparecer minha primeira alteração e o que desejo fazer, depois disso vai aparecer minha segunda alteração e o que desejo fazer.

-->git status 
Vai mostrar o status das alterações na branch

-->git show
Vai mostrar o que foi alterado

-->git commit -m <"..."> 
Vai titular o commit 1

Se eu der "git log" vai mostrar o histórico dos commits, lá vou ver que apenas o commit 1 foi lançado, enquanto que o 2 está esperando aprovação.

Daí posso lançar:
--> git add <arquivo a ser commitado>
Que será a segunda alteração feita no mesmo arquivo e lançada como outro commit.

```shell
git status
```
Para verificar o arquivo

`git commit -m <"...">`
Para lançar o commit e seu título

```
git log
```
Para verificar o histórico de commits

# Como juntar commits por interatividade ?
`git rebase -i -HEAD~<posição do commit a ser juntado>`

Antes de tudo `git log`para ver quais commits eu tenho. Achei os commits q quero juntar ? Sim, dou `git rebase -i -HEAD~2`(onde, `-i`quer dizer que o rebase é interativo e `-HEAD~2`quer dizer que escolhi o commit que está no HEAD e o segundo).

Ex.: 
    Como juntar 2 commits que estão no histórico e não sei quais são?
    Mole. `git log` vejo as hashs que quero juntar. 
    Dou `git rebase -i HEAD~2`(rebase além de juntar branchs tb serve para trabalhar com histórico), isso vai mostrar os dois últimos em uma tela, lá terá as opções de como posso juntá-los.
    Defino como um commit será ajustado em relação ao outro e, se estiver usando o vi, ao final da página insiro `:wq` para editar a mensagem do commit, já se estiver usando o nano, ^x, y, enter. Com o nano para fechar a união dos commits uso `git commit --amend` para editar a mensagem do commit, se for o caso, e fechá-lo. Deu Kaô ? `git rebase --continue` ou `git --edit-todo`.

# Como juntar commits com Fixup e Autoquash ?
`git commit -fixup <hash do commit corrigido>

O que isso quer dizer?
Fiz um commit (sem dar push), logo em seguida fiz outro consertando o anterior.
    `git log` para ver a hash do commit a ser corrido
    `git add <. ou arquivo>`
    `git commit -fixup` <hash do commit q foi corrigido>
Lmebrando que para ver o histórico e a hash de um commit damos `git log`.   git log

    Simulação:
    git add .
    git commit -m "a"
    git add .       (consertei commit a e add algo)
    git commit --fixup <hash de a>
    git add .       (consertei commit ab e add algo)
    git commit --fixup <hash de ab>
    Mas agora eu tenho 3 commits de um mesmo trecho, como juntá-los em um só?
    git log (para ver a hash do commit anterior a "a", que foi o primeiro)
    git rebase -i --autosquash <hash do commit anterior a "a">
            (dessa maneira vamos pegar o "a" e seus fixup e fazer um autosquash)

# Resolvendo conflitos na mao
    Situcao hipotetica:
    Fiz x alteracoes no meu vscode e um colega de trabalho fex y alteracoes na plataforma git. Ao puxar os arquivos para o meu repositorio local, ("git pull <remoto> <local>"), pode haver conflitos entre as alteracoes realizadas, apos a resolucao dos conflitos, usamos o comando `git merge --continue`, para mesclar as alteracoes e estando ok `git push <local> <remoto>`

# Usando autocorrect
Parra corrigir erros de digitacao nos comandos do git.

`git config --global help.autocorrect 1` ou `git config --global hep.autocorrect true`

# Como zipar um repositorio
`git archive <branch> --format=zip --output=<nomedoarquivo.Zip>`

Ex.: Transformando a branch master em um arquivo zip
`git archive master --format=zip --output=master.zip` 

Zipa todo um repositorio

# Git Log - mudando visual
`git log --pretty=oneline`
Deixa o hash e a informacao de commit em uma linha so

`git log --pretty=oneline --graf`
Mostra o historico de mudancas por branchs nos commits pretty=oneline

`git log --pretty=oneline --grahistoricof --all`
Mostra todo o historio dos branchs nos hashs, incluindo o stash

# Filtros no Git Log
`git log --since=<data(Jan 1 2018)>`
Vai listar todos os logs DESDE o dia 1 de janeiro de 2018

`git log --until=<data(jan 1 2018)>`
Vai listar todos os logs ATE o dia 1 de janeiro de 2018

`git log --since=<data(Jan 1 2018) --until=<data(Jan 10 2020)>`
Vai listar os logs DESDE o dia tal ATE o dia tal

`git log --author=<name>`
Todos os commit do autor x

`git shortlog`
Vai mostrar o autor e todos os commits 

`git shorlog -sn`
Mostra a quantidade de commits e seu autor

`git log -3`
Vai mostrar os 3 ultimos commits

# GIT REFLOG - o salvador
`git reflog`
Mostra todos os tipos de alteracoes realizadas no repositorio, com ele e possivel recuperar hashs deletadas e traze-las de volta a vida.

```shell
Situacao:
`git reset --hard <hash>` 
`git reflog` vamos quem vc quer salvar e trazer de volta a vida, pega o hash dele taca no reset --hard (reset do reset)
`git reset --hard <hash>`



Comentar e fechar uma issue

No comentario "#" darah opcao de refenciar tal issue gerando um link de fechamento apos conclusao da issue

Ao final do comentario a inclusao de "-Closes #1,2 ou 3" referenciaara tal issue a ser finalizada


Pull Request
Nada mais he do que um commit separado que faz alusao ao master


issue sao os comentarios e resolucoes e pull request eh o pedido ou inclusao da solucao



Criando tabela em um comentario

|titulo1|titulo2|
|-------|-------|
|link1|link2|


O que eh e quais sao os workflows  do git ?
Workflow eh passo-a-passo das tarefas no git do desenvolvimento a producao.

- Centralized Workflow
- Featrure Branch Workflow
- Gitflow Workflow

--Centralized Workflow
 Funciona com um branch soh.
 Funciona com equipe pequena - por causa de facilidade de conflitos
 Eh necessario sempre ficar dando git pull e mais ainda git gull <remoto> <local> --rebase
 Pq ? 
 Pq o git pull --rebase leva a ultima alteracao pra cima do historico.
 (ex.: a finalizou sua feature e commitou, b apos a terminou sua feature e commitou. Mesmo que nao haja confloto vai dar ruim pq aconteceu uma mudanca antes, b tem d baixar `git pull <remoto> <local> --rebase, para trazer as alteracoes de a para dps colocar as suas, assim ela fica no topo das mudancas)



--Feature Branch Workflow
 Um branch para cada feature.
 Quando a feature estah pronta daih sim pull request pro master.
 O Pull request passando pelo code review, estando tudo ok faz um maerge pro master.
 Evita conflitos e e permite trabalhos paralelos. (sempre tem de manter seu master atualizado)
 

-- Git Flow
 Trabalha tanto em repositorio novos quanto ja existentes.

 `git flow init`
 Dai pergunta qual sera o branch padra o de producao [master]
 qual sera o branch de desenvolimento [develop]
 qual sera os prefixos:
   para branch de feature [feature/]
   para branch de release[release/]
   para branch de hotfix [hotfix/]
   para branch de support [support/]
   para branch de tag [ ] (pode ser definido conforme necessario

 Apos esses primeiros passos ja cai direto na branch develop

 como a primeira feature sera a index
 -> `git flow feature start <nome da feature (update-contact)>` <-
 Vai trocar para a nova branch (update-contact)
 Pode comecar a commitar na branch,
 -> git add . <-
 -> git commit -m <"mensagem"> <-
 Finalizada as acoes, para subir para o git hub para pedir pull request
 -> git flow feature publish <nome da feature (update-contact> <-
 Pq publish ?
 Pq a feature vai para avaliacao para posterior publicacao.

 Atencao:
 Pelo git flow devemos sempre dar o pull request para o develop, NAO para o master.
 Entao, no git hub, ao criar o pull request haverah  duas abas: base e compare.
 A aba compare vai jogar a feature que pediu o pull request (update-contact).
 A aba base, sempre sera o develop.
 Se a branch develop nao estiver dispinivel, eh pq ainda nao foi dado push nela do terminal para o github. Como resolver ? 
 Mole. 
 -> git checkout develop <- para entrar na branch develop
 -> git push origin develop <- para subir a branch develop para o github

 Criado o pull request:
 Passa pelo code review.
 Estando tudo certo, volto para o terminal. 

 ->git checkout - <- para voltar a branch anterior
 -> git flow feature finish <nome da feature (update-contact)) <- 
 Pq finish ?
 Pq agora a feature esta finalizada, ja foi avaliada (publish) e pronta para ser publicada (finish).

 Feito isso, o git flow mergea a feature com o delevop, remove a branch de desenvolvimento (update-contact) e entra na branch develop.
 Dai na develop, com tudo certo, damos o push
 -> git push origin develop <-
 Pronto, mergeado. Apos isso, nao esquecer de deletar o branch de desenvolimento concluido do repositorio remoto. Dando refresh no pull request, vai aparecer a opcao de deletar a branch e tchau.


 Criando um RELEASE:
 Release eh jogar para producao, ou seja, do develop para o master.

 -> git flow release start <nome do release (em geral por versao)> <-
 Estando tudo pronto.
 -> git flow release finish <nome do release> <-
 Dai vai criar um commit de merge com descricao e mensagem, depois pede uma mensagem de tag, dem geral essa mensagem de tag eh o nome do release.
 <- git push origin master --tag <-
 Vai jogar tudo para o master, release e tag.
 Tambem tem d ir ao develop e dar git push para mante-lo atualizado.
 <- git push origin delevop <-


 Trabalho rodando, tudo ok, PAH... tem bug.
 Criamos um HOTFIX.
 -> git flow hotfix star fix-<nome do fix> <-
 Apos a correcao
 -> git add <-
 -> git commit -m <mensagem> <-
 -> git flow hotfix finish <nome do hotfix) <-
 Dai vai dar merge, mostrar as mudancas e a mensagem, vai pedir a mensagem pra tag e vai apagar o hotfix.
 
 Feito isso voltemos ao master.
 -> git checkout master <-
 -> git push origin master --tags <-
 Vai subir geral, mudanca e fix.


 GH-PAGES
 PAGINA NO GITHUB
 -> git checkout -b gh-pages <-
 -> git push origin gh-pages <-
 Vai botar no ar um site utilizando o github.


`git checkout master`
`git checkout -b <branch>`




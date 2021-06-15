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

# Como juntar commits ?
Antes de tudo `git log`para ver quais commits eu tenho. Achei os commits q quero juntar ? Sim, pego a hash deles.

Ex.: 
    Como juntar 2 commits que estão no histórico e não sei quais são?
    Mole. `git log` vejo as hashs que quero juntar. 
    Dou `git rebase -i HEAD~2`(rebase além de juntar branchs tb serve para trabalhar com histórico), isso vai mostrar os dois últimos em uma tela, lá terá as opções de como posso juntá-los.
    Defino como um commit será ajustado em relação ao outro e, se estiver usando o vi, ao final da página insiro `:wq` para editar a mensagem do commit. Se estiver usando o nano ^x, y, enter. Com o nano para fechar a união dos commits uso `git rebase --continue`para editar a mensagem, se for o caso, e fechar o commit.
         
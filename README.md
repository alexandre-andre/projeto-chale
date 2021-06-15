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

git reset --hard <numero da log>
Volta para o commit tal e ignora -apaga- todos os commits após este

git reset --soft <numero da log>
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
git log - para ver o log do commit
git show <log do commit> para mostrar a alteração 

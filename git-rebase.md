## Usando git rebase

É comum durante o desenvolvimento gerar mais de um commit na branch. Com o [git rebase](https://git-scm.com/docs/git-rebase) é possível juntar todos eles em um único commit para enviar o merge request e manter um histórico limpo de alterações.

[Veja um exemplo de merge request com vários commits](https://github.com/adhenawer/testes/pull/1/commits)

[Agora veja após o git rebase](https://github.com/adhenawer/testes/pull/2/commits)

### Abaixo o passo-a-passo para execução do rebase

No exemplo foram usados 3 commits

```
$ git commit -m "#3 commit"

$ git commit -m "#4 commit" 

$ git commit -m "#5 commit" 
``` 

Após ter feito todos os commits execute o rebase:

```
$ git rebase -i HEAD~3
```

### Irá abrir os commits que vão ser mergeados

```
pick 86a2e56 #3 commit
pick 8ea78b5 #4 commit
pick d2ed1cd #5 commit

# Rebase b02e286..d2ed1cd onto b02e286 (3 commands)
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

### Deixe o primeiro commit como pick e os demais como s (squash)

```
pick 86a2e56 #3 commit 
s 8ea78b5 #4 commit
s d2ed1cd #5 commit
``` 

Salve a alteração (**:x!**)

### No próximo passo, altere o texto padrão do git rebase pela descrição desejada do seu commit e salve novamente (**:x!**). Exemplo:

#### De *mensagem padrão do git*
```
# This is a combination of 3 commits.
# This is the 1st commit message:

#3 commit

# This is the commit message #2:

#4 commit

# This is the commit message #3:

#5 commit
``` 

#### Para *sua mensagem*

```
Commits [#3, #4, #5]
```

### Você deve receber o retorno

```
detached HEAD f3084e0] Commits [#3 #4 #5]
 Author: Rodolfo Moraes <adhenawer@MacBook-Air-de-Rodolfo.local>
 Date: Sun May 21 14:59:57 2017 -0300
 1 file changed, 3 insertions(+)
Successfully rebased and updated refs/heads/com-rebase.
```

Agora basta enviar seu push para o repositório principal.

:warning: Caso já tenha feito push anteriormente, será necessário forçar (git push -f)

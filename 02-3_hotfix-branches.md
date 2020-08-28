# Hotfix Branch (Branch de correção)

## Criando uma hotfix branch

Branches de correção são criados a partir do branch master. Por exemplo, digamos que a versão corrente é a 1.2.0 e está causando problemas devido a um erro grave em produção. Porém as mudanças no branch develop não estão estáveis ainda. Precisamos criar um branch de correção e começar a corrigir o problema.

    $ git checkout -b hotfix/1.2.1 master
    Switched to a new branch “hotfix/1.2.1”

    $ ./bump-version.sh 1.2.1
    Files modified successfully, version bumped to 1.2.1.

    $ git commit -a -m “Bumped version number to 1.2.1”
    [hotfix-1.2.1 41e61bb] Bumped version number to 1.2.1
    1 files changed, 1 insertions(+), 1 deletions(-)

Não esqueça de aumentar a versão após criar o branch.
Em seguida corrigir o bug e comitar em um ou mais commits.

    $ git commit -m “Fixed severe production problem”
    [hotfix-1.2.1 abbe5d6] Fixed severe production problem
    5 files changed, 32 insertions(+), 17 deletions(-)

---
## Finalizando um branch de correção

Quando finalizados as correções, o branch deve ser mesclado devolta com o branch master, mas também deve ser mesclado com o branch develop, para que as correções sejam incluídas na próxima versão também. O processo é similar ao do branch de lançamento.

Primeiro atualize o master e crie uma tag.

    $ git checkout master
    Switched to branch ‘master’

    $ git merge --no-ff hotfix/1.2.1
    Merge made by recursive.
    (Summary of changes)

    $ git tag -a 1.2.1

Em seguida inclua a correção no branch develop.

    $ git checkout develop
    Switched to branch ‘develop’

    $ git merge --no-ff hotfix/1.2.1
    Merge made by recursive.
    (Summary of changes)

A única excessão a esse processo é quando existe um `branch de lançamento`, neste caso as alterações devem ser mescladas nele, ao invés de no branch develop. As alterações mescladas no branch de lançamento refletirão no banch develop também, quando forem finalizadas. Se o branch develop precisar da correção imediatamente e não puder esperar a finalização do branch de lançamento você pode mesclar com ele também.
Finalmente, removemos o branch já mesclado:

    $ git branch -d hotfix/1.2.1
    Deleted branch hotfix/1.2.1 (was abbe5d6).
---
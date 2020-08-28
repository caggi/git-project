# Release Branch (Branch de lançamento)

## Criando uma release branch

Branches de lançamento são criados a partir do branch develop. Digamos que o projeto está na versão 1.5.3 e há uma implantação em breve. O estado do branch develop está pronto para a próxima implantação e decidimos que vai se tornar 1.2.0 (ao invés de 1.1.5 ou 2.0.0). Então criamos um branch com o nome da versão que escolhemos.

        $ git checkout -b release/1.2.0 develop
        Switched to a new branch “release-1.2.0”

Depois de criar o branch, a primeira coisa a fazer é aumentar a versão nos arquivos equivalentes e comitar. Podendo ser um `composer.json, defines.mk, um version.py, etc`. Esta alteração é chamada de bump.

        $ ./bump-version.sh 1.2.0
        Files modified successfully, version bumped to 1.2.0

        $ git commit -a -m “Bumped version number to 1.2.0”
        [release/1.2.0 74d9424] Bumped version number to 1.2.0
        1 files changed, 1 insertions(+), 1 deletions(-)

Neste exemplo o script `bump-version.sh` faz estas alterações, mas podem ser feitas manualmente.

Este branch deve existir por enquanto, até que esteja pronto para ser implantado definitivamente em produção. Pequenas correções são permitidas nele (ao invés do branch develop). Adicionar funcionalidades novas nele são proibidas, apenas correções pontuais desta versão de lançamento.

---
## Finalizando uma release branch

Quando o branch de lançamento estiver pronto para ser implantado em produção, algumas ações precisam ser tomadas. Primeiro o brach de lançamento é mesclado com o branch master (uma vez que cada commit no master é uma nova versão, por definição):

        $ git checkout master
        Switched to branch ‘master’

        $ git merge — no-ff release/1.2.0
        Merge made by recursive.
        (Summary of changes)

Em seguida este commit deve ser tageado para referência futura para esta versão:
        
        $ git tag -a 1.2.0

Finalmente, as mudanças feitas no branch de lançamento precisam mescladas devolta no branch develop, para que as versões futuras também possuam as correções feitas neste branch:

        $ git checkout develop
        Switched to branch ‘develop’

        $ git merge — no-ff release/1.2.0
        Merge made by recursive.
        (Summary of changes)

Neste momento podem ocorrer alguns conflitos, já que as correções podem mudar a versão dos arquivos, se acontecer, corrija e comite.
Feitos os merges podemos excluir o branch de lançamento, já que não precisamos mais dele:

        $ git branch -d release/1.2.0
        Deleted branch release/1.2.0 (was ff452fe).

---
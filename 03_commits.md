# PGC - Commits

## Estrutura de um Commit (mensagem de confirmação)

Qualquer linha da mensagem de confirmação não pode ter mais de 100 caracteres! Isso permite que a mensagem seja mais fácil de ler.

Uma mensagem de confirmação consiste em um cabeçalho, um corpo e um rodapé, separados por uma linha em branco.

    [cabeçalho obrigatório]
    linha em branco
    [corpo opcional]
    linha em branco
    [rodapé(s) opcional]

---
## Cabeçalho da mensagem

O cabeçalho da mensagem é uma única linha que contém uma descrição sucinta da mudança contendo um `tipo`, um `escopo` opcional e um `assunto`.

    <tipo obrigatório>[escopo opcional]: <assunto obrigatório>
    linha em branco
    [corpo opcional]
    linha em branco
    [rodapé(s) opcional]

- `<tipo>` permitido: Isso descreve o tipo de mudança que este commit está fornecendo.
    - feat    : (recurso)         um commit do tipo feat introduz um novo recurso para a base de código (isso se correlaciona com MINOR no versionamento semântico);
    - fix     : (correção de bug) um commit do tipo fix corrige um bug em sua base de código (isso se correlaciona com PATCH no controle de versão semântico);
    - docs    : (documentação);
    - style   : (formatação, ponto e vírgula faltando, ...);
    - refactor : (refatorações) ;
    - test    : (ao adicionar testes ausentes);
    <!-- - chore (maintain) -->
    - BREAKING CHANGE: um commit que tem um rodapé BREAKING CHANGE: ou anexa um `!` após o tipo ou escopo, introduz uma alteração que pode provocar uma interrupção. Esse tipo de alteração é comumente relacionado a alteração na estrutura de API's ou banco de dados (correlacionando com MAJOR no controle de versão semântica). A BREAKING CHANGE pode fazer parte de commits de qualquer tipo.

    - `<escopo>` permitido: O escopo pode ser qualquer coisa para fornecer informações contextuais adicionais como especificação do local da mudança do commit.

- `<assunto>` : Esta é uma breve descrição da mudança.
    - use o tempo imperativo do presente: “muda” e não “mudar” nem “mudanças”;
    - não coloque a primeira letra em maiúscula;
    - sem ponto (.) no final.

- `corpo` da mensagem : assim como em `<assunto>`, use imperativo do presente: “muda”, não “mudar” nem “mudanças”.
    - inclui motivação para a mudança e contrastes com o comportamento anterior.


- `rodapés` : Utilizados para adicionar informações estruturadas em mensagens de commit.
    - `deve ser informado no rodapé o identificador do requisito equivalente as alterações realizadas no commit;`
    - `git-interpret-reboques` permite analisar informações estruturadas em mensagens de commit;
    - instruções sobre `BREKING CHANGE` precisam ser descritas no rodapé das mensagens de commit.

<!-- ## git-interpret-trailers -->

---
## Exemplos de mensagem

Commit para adição de recurso com apenas cabeçalho

    feat: adiciona função de login e logout

    requisito: [m3#12.1] [m3#12.2]

Commit para adição de recurso com cabeçalho e corpo

    feat: adiciona estrutura da visualização do plano de estudo

    adiciona o fluxo de navegação da telas presentes no módulo de plano de estudo e realiza a 
    integração com a API tornando o fluxo de visualização funcional porém sem as informações
    dinâmicas que estão cadastradas no banco.

    requisito: [m3#15.1]

Commit para correção de recurso com cabeçalho

    fix: dinamiza informações da visualização do plano de estudo

    atualiza implementação dos componentes da visualização do plano de estudo para receber as
    informações dinâmicas que estão cadastradas no banco (informações template, pois ainda falta
    implementar a função de cadastro do plano de estudo).

    requisito: [m3#15.1]
---
# Introdução ao Controle de Versão com Git e GitHub

Referência básica:

1. [Tutoria Oficial](https://git-scm.com/docs/gittutorial)

2. [Documentation](https://git-scm.com/doc)

3. [Everyday Git Standalone](https://git-scm.com/docs/giteveryday#STANDALONE)
4. [Git Cheat Sheet](https://training.github.com/downloads/github-git-cheat-sheet.pdf)
5. [Visual Cheat Sheet](https://ndpsoftware.com/git-cheatsheet.html#loc=index;)
6. [GitHub Training Manual](https://githubtraining.github.io/training-manual/#/01_getting_ready_for_class)
7. [GitHub Documentation](https://docs.github.com/pt)
8. [git tutorial nulab](https://nulab.com/learn/software-development/git-tutorial/)
9. [No Bullshit GitTutorial](https://up1.github.io/git-guide/index.html)
10. [Think like a Git](https://think-like-a-git.net/)

## O processo de controle de versão ou versionamento

Versionamento é o processo de configuração de software que consiste em controlar as edições dos artefatos produzidos ao longo do processo de software.

## O método de controle de controle de versãoi

Há apenas um diretório chamado principal.  Este diretório é atualizado diretamente por meio de pull requests onde o arquiteto de software e/ou techlead fazem o Code Review.  Todo pull request de uma funcionalidade só pode ser feito após passar por testes unitários e de integração.

## Usando a ferramenta de controle de versão Git com repositórios GitHub

O Git é uma ferramenta de controle de versão que controla o conteúdo dos arquivos e não os arquivos propriamente ditos, ou seja, é preciso dizer qual arquivo está sendo alterado, mas o intuito é controlar o conteúdo do mesmo.

O básico do uso diário do Git pode ser visto em [Git Everyday](https://git-scm.com/docs/giteveryday) onde se mostra o que cada participante de um projeto precisa saber quer seja ele um desenvolvedor individual, um membro de uma equipe, um lider técnico que integra o projeto ou um gestor de repositório.

### Configurando o Git

Em primeiro lugar, especifique o usuário do Git com os comandos abaixo:

`git config --global user.name "seu nome"`
`git config --global user.email "seu email"`

### Inicializando o controle de versão de um projeto

No diretório do projeto que você está desenvolvendo, digite:

`git init`

### Adicionando arquivos ao controle de versão do Git

Para adicionar todos os arquivos do projeto, digite:

`git add .`

Diz-se que os projetos estão na "staging area".  Os projetos na "staging area" estão ali apenas temporariamente, isto é, eles não estão na árvore de arquivos controlados pelo Git.

Para adicionar apenas um arquivo específico ao controle do git, digite:

`git add nome_do_arquivo`

Se quiser adicionar mais de um arquivo, digite:

`git add arquivo1 arquivo2 arquivo3`

Não há limite para o número de arquivos que podem ser adicionados ao controle.

### Confirmando o que será comitado

`git diff --cached`

Um sumário do que será comitado pode ser visto em:

`git status`

### Armazenando permanentemente um arquivo à árvore de controle do Git

`git commit -m "mensagem que caracteriza o commit"`

### Fluxo básico de trabalho

1. crie o diretório de projeto
2. use git init para controlar o repositório do projeto
3. use git add . para colocar todos os arquivos em stage
4. use git commit -m "mensagem" para guardar definitivamente as alterações
5. repita o realizado em 2, 3 e 4.

### Vendo o histórico do projeto

Use:

`git log`

Vendo detalhadamente as modificações

`git log -p`

Vendo um sumário das mudanças

`git log --stat --summary`

### Gerenciando branches

Esta é uma funcionalidade que não gosto de usar no meu fluxo de trabalho, mas vou aprender o básico assim mesmo.

Um branch é um galho na árvore de controle o git.  Veja o git com uma árvore de um sistema de arquivos, mas o que a árvore armazena não é o arquivo mas o conteúdo do arquivo.  Assim, quando se cria um branch, tudo se passa como se tivesse sido criado um galho (isto é, um "subdiretório") da árvore de controle do git.

Vamos fazer o exemplo constante em [gittutorial - A tutorial introduction to Git](https://git-scm.com/docs/gittutorial#_managing_branches)

#### Criando um branch

`git branch nome_do_branch`

#### Visualizando a lista de branches

`git branch`

#### Mudando de branch

O branch atual fica com um asterisco na lista de branches do git branch.  Para mudar de branch digite:

`git switch nome_do_branch para o qual se deseja ir`

Observe que mudanças feitas em um branch não se refletem em outros.  Então, é preciso comitar no novo branch quando se muda de branch.  O melhor mesmo seria fazer um merge como se verá mais tarde.

#### Misturando branches com merge

`git merge nome do branch que se deseja misturar com o branch atual`

#### Apagando branches

`git branch -d nome_do_branch a ser apagado`

### Colaborando com outros desenvolvedores (GitHub)

Referência; [Using Git for collaboration](https://git-scm.com/docs/gittutorial#_using_git_for_collaboration)

Suponha que Alice tenha um repositório Git em /home/alice/project e que Bob - que possui o diretório /home/bob/ na mesma máquina vai contribuir com o projeto.  Para isto acontecer, o seguinte procedimento deverá ser adotado.

1. Bob, estando em seu diretório /home/bob/, dá o seguinte comando: `git clone /home/alice/project myrepo`
Isto cria um repositório denominado myrepo que é uma cópia do repositório de Alice, ou seja, a árvore de conteúdo do repositório de Alice está exatamente igual no repositório myrepo

2. Bob faz as modificações que quiser em myrepo, as comita com `git commit -a` ou `git add .` e `git commit -m "mensagem"` e avisa Alice que está pronto.

3. Alice, estando dentro do repositório de seu projeto, isto é, em /home/alice/project, puxa o repositório myrepo de Bob usando o seguinte comando

`git pull /home/bob/myrepo master`

Este comando fará um merge do branch master do repositório myrepo de Bob com o branch ativo do repositório de Alice.

### O repositório remote

Quando se trabalha com um repositório várias vezes, este é pode ser chamado de **remote** para facilitar o trabalho de pull.  Por exemplo, o repositório de Bob pode se tornar o repositório remote de Alice.  Para tal, Alice precisa digitar:

`git remote add bob /home/bob/myrepo`

Agora, a árvore do repositório myrepo de Bob passa a ser chamada de remote com apelido bob.  Para Alice pegar as alterações de myrepo *sem fazer merge com seu código* basta usar:

`git fetch bob`

**Observação**
Git foi pensado para colaboração direta entre desenvolvedores, mas pode ser usado para alimentar um repositório central.  Quando Bob clonou o repositório de Alice, git armazenou as configurações deste repositório como git config --get remote.origin.url /home/alice/project.

Se Bob resolver trabalhar em outro repositório, ele pode usar protocolo ssh para fazer clones e pulls com `git clone alice.org:/home/alice/project myrepo` ou usando git pull com protocolo nativo do Git ou ainda http.

Usando git push pode-se usar Git para alimentar um repositório central.  Ver mais sobre isso em [git push](https://git-scm.com/docs/git-push).

### Explorando a história

Referência: [link](https://git-scm.com/docs/gittutorial#_exploring_history)

Lembremos que o comando `git log` mostra a sequência de commits de um repositório.

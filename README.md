# Resumo de comandos do GitHub para o uso no dia-a-dia

### Configurações iniciais

```sh
$ ctrl + l  ou  clear // Limpa Terminal

// Lista todas as configurações
// global: todos usuários e todos repositórios (/etc/gitconfig)
// local : específicas para um repositório (.git/config)
// system: todos usuários (/etc/gitconfig)
$ git config --list
$ git config --global user.name "Nome Sobrenome" //	Define usuário
$ git config --global user.email seuemail@email.com // Define e-mail
$ git config --global init.defaultBranch main // ao iniciar um repositório, a branch principal será main ao invés de master	
```

### Autenticação via Token

```sh
// comando para criar uma cópia local do repositório remoto
// não possui acesso
$ git clone https://...

// criar token: github > superior direito foto > settings > Developer settings > Personal access tokens > tokens (classic) > generate new token (classic)
copiar código
	
$ git clone https://... // (na senha colocar o código copiado do token)
$ git config credential.helper store // (armazena global em /etc/gitconfig ou ~/.git-credentials)
$ git clone https://...

$ git config --global credential.helper
$ git config --global --show-origin credential.helper  //C:\Users\rafael\.gitconfig
```

### Autenticação via ssh

```sh
// github > superior direito foto > settings > SSH and GPG Keys (documentação com tutorial)

$ ls -al ~/.ssh
$ ssh-keygen -t ed25519 -C "leticiorafael@gmail.com"
$ eval "$(ssh-agent -s)" //start ssh-agent in the background
$ ssh-add ~/.ssh/id_ed25519 //adiciona chave ssh privada ao ssh-agent

github > superior direito foto > settings > SSH and GPG Keys > New SSH > colocar chave publica
cd ~/.ssh
ls
cat id_ed25519.pub

$ git clone git@github.com:... "SSH"
```

### Criando e clonando repositórios

```sh
mkdir repo-local
cd repo-local

// Inicia um repositório git vazio
// cria .git
// cria branch inicial sem nenhum commit
$ git init
cd .git	//diretório oculto
ls

// comando para criar uma cópia local do repositório remoto
// não é necessário usar o git init
$ git clone https://...  
$ git clone https://... repo-clonado //muda o nome do diretório

cd repo-clonado
cd .git
cat config
cd ..
$ git remote add origin https://github.com/... //vincula o diretorio local com o remoto "origin é o local remoto"

cd .git
cat config //consulta que está vinculado ao diretório remoto

adicional: copiar branch sem ser a main
$ git clone URL --branch feature-1 --single-branch

$ git push -u origin main //-u associa o branch local ao branch remoto, origin diretório remoto, main branch local enviada ao remoto
```

### Salvando alterações no repositório local

```sh
mkdir dio-resumos-git-e-github
cd dio
$ git init

$ git status
touch READNE.md
$ git status

$ git add README.md //adiciona arquivo específico
$ git add . //adiciona todos os arquivos que ainda não foram adicionados

$ git commit -m "commit inicial"
$ git log

mkdir resumos
$ git status
touch resumos/resumo-aula1.md //não reconhece diretórios vazios, apenas com arquivos
echo resumos/ > .gitignore //adiciona pasta no gitignore para ser ignorado

touch aulas/.gitkeep //arquivo para reconhecer o diretorio se não possuir arquivos
```

### Desfazendo alterações no repositório local

```sh
rm -rf .git

$ git status
$ git restore README.MD  //descarta alterações e volta o arquivo para o ultimo commit
$ git status

$ git commit --amend -m "adiciona aaa..." //altera a mensagem do último commit
$ git commit --amend //abre editor

$ git log // mostra os commits

//copiar o código do commit ex:4234y2g34ui2y3g4i2uy3g4
$ git reset --soft 4234y2g34ui2y3g4i2uy3g4 //apaga o commit

$ git reset --mixed código penultimo commit //padrão 
$ git reset --hard código penultimo commit

$ git reflog //mostra histórico de reset
```

### Enviando e Baixando alterações com o Repositório Remoto

```sh
criar repositório no github
$ git status
$ git add .
$ git status
$ git commit -m "commit local para enviar"
$ git log //mostra os commits
$ git remote add origin https://...
$ git branch -M main
$ git push -u origin main

$ git pull //mescla remoto com o local
```

### Trabalhando com Branches - Criando, Mesclando, Deletando e Tratando Conflitos

```sh
//Branches apontam para um determinado commit
// mesclar faz as branchs apontar para o mesmo commit

$ git checkout -b teste //troca de branch
$ git log /consultar commit

echo "commit-3-branch-teste" > commit-3-branch-teste
$ git add .
$ git commit -m "commit-3"

$ git checkout main //volta para a branch main

$ git branch -v //mostra os commits de cada branch

$ git merge teste //mescla a teste com a branch atual que é a main

$ git branch //mostra as branchs
$ git branch -d teste //exclui a branch teste

------------------------------
Conflitos de merge:
------------------------------
2 pessoas enviam gera conflito

$ git log
//alterar arquivo no local e alterar arquivo no remoto com commits

$ git push origin main
//rejeita porque remotamente contém trabalho que não possui localmente

$ git pull //o arquivo diferente vai possuir os 2 conteúdos
//decidir qual alteração quer no próprio arquivo e salvar

$ git status //mostra arquivo alterado
$ git add. //adiciona a alteração
$ git commit -m "commit após o conflito"

$ git log

$ git push origin main //envia
```

### Comandos úteis

```sh
//git pull -> git fetch + git merge

$ git log
$ git fetch origin main
$ git diff main origin/main //mostra diferença
$ git merge origin/main

git clone https://... --branch teste --single-branch  //clona outra branch ao invés da principal

$ git stash //arquivo a modificação
$ git stash list
$ git checkout -b teste2 //nova brench sem a modificação
$ git checkout teste //
$ git stash list
$ git stash pop //tras as alterações
$ git stash apply // manter
```


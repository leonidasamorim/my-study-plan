# :rocket: Heroku Tutorial 

O tutorial abaixo lista os comandos heroku que mais tenho usado. 

## - Criando um Projeto - Staging

```
$ heroku login 

$ heroku apps:create nomaproject-staging
```
- [Tutorial](https://devcenter.heroku.com/articles/creating-apps)

## - Fazendo Deploy  - (Usando url projeto)

O Exemplo abaixo é usando a url do prejeto do heroku, em uma branch `main` nomeando o repositório remoto de `staging`

```
Ex: git remote add {remote} {url}

$ git remote add staging https://git.heroku.com/dressall-staging.git

$ git push staging main
```

- [Tutorial](https://devcenter.heroku.com/articles/git)

## - Heroku Bash 

Esse comando consegue acessar a raiz do projeto direto no ambiente remoto do heroku  

```
$ cd pasta-do-projeto

$ heroku run bash -a nome-projeto 
```

## - Heroku Logs 

Esse comando permite ver o acesso aos logs das requests no servidor remoto

```
$ cd pasta-do-projeto

$ heroku logs -t -a nome-projeto 
```

## - Rails Console

Esse comando permite acesso ao rails console no servidor remoto

```
$ cd pasta-do-projeto

$ heroku run rails c -a nome-projeto
```

## - Agendar Backup Postgres

Esse comando agenda os backups do banco de dados postgres

```
$ cd pasta-do-projeto

$ heroku pg:backups:schedule DATABASE_URL --at '04:00 America/Sao_Paulo' --app nome-projeto

$ heroku pg:backups:schedules --app nome-projeto
```

## - Restaurar um Backup Postgres

Esse comando restaura um backup em uma aplicação com banco já existente. Obs: `a000` É o arquivo do backup no heroku que foi feito previamente.

```
$ cd pasta-do-projeto

$ heroku pg:backups:restore a004 HEROKU_POSTGRESQL_GRAY_URL --app nome-projeto

```

## - Migrar um banco de Hobby-dev para hobby-basic

Esse comando faz a migração do banco sem perder os dados. Obs: a variável `DATABASE_URL` é a url do banco antigo. 

```
$ cd pasta-do-projeto

$ heroku maintenance:on -a nome-projeto

$ heroku addons:create heroku-postgresql:hobby-basic -a nome-projeto

$ heroku pg:copy DATABASE_URL HEROKU_POSTGRESQL_JADE_URL -a nome-projeto

$ heroku pg:promote HEROKU_POSTGRESQL_JADE_URL -a nome-projeto

$ heroku maintenance:off -a nome-projeto

```

## - Resetar uma base de dados Postgres

Esse comando o reset da base de dados e depois restaura migrations e seed. 

```
$ cd pasta-do-projeto

$ heroku pg:reset DATABASE_URL --confirm nome-projeto

$ heroku run rake db:migrate --app nome-projeto

$ heroku run rake db:seed --app nome-projeto

```

## - Fazer backup de um banco remoto para máquina local

Esse comando vai salvar um dump do banco remoto na raiz do seu projeto com o nome `latest.dump`. 

```
$ cd pasta-do-projeto

$ heroku pg:backups:capture -a nome-projeto

$ heroku pg:backups:download -a nome-projeto

```

## - Restaurar um banco de dados remoto em um banco local (Em projetos rails + postgres)

Esse comando vai restaurar o conteúdo de um um dump do banco remoto no banco de dados local da máquina. 

```
$ cd pasta-do-projeto

$ rails db:drop db:create

$ heroku pg:backups:capture -a nome-projeto

$ heroku pg:backups:download -a nome-projeto

$ pg_restore --verbose --clean --no-acl --no-owner -h localhost -U meu-user-maquina-local -d nome_banco_local_maquina_development latest.dump

$ rails db:migrate RAILS_ENV=test

$ rails db:migrate RAILS_ENV=development

```

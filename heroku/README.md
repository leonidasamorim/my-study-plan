# Heroku Tutorial 

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

## - Heroku Bash - Acessar a raiz do projeto remoto

```
$ heroku run bash -a nomeprojeto-staging 
```


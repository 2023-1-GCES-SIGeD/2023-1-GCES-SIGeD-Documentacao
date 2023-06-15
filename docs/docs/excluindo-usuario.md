<h1 style='text-align: center;'>Excluindo usuário no banco de dados</h1>

## Introdução

Este guia tem como objetivo auxiliar novos desenvolvedores no processo de exclusão de usuários no banco de dados e utiliza o repositório [Backend users](https://github.com/DITGO/2021-2-SiGeD-Users).     
Tal processo é relevante quando ocorre algum erro no envio da senha temporária para determinado e-mail e, para enviar a senha temporária para este mesmo e-mail, é necessário criar o usuário novamente, porém ocorrerá o erro de usuário/e-mail já existente.

## Entrando no shell

Após [subir o ambiente](https://github.com/2023-1-GCES-SIGeD/2023-1-GCES-SIGeD-Documentacao/blob/main/docs/docs/subindo_o_ambiente.md), entre no _shell_ do container de banco de dados de usuários (db_users). Acesse o container de banco de dados de usuários:     

```bash
sudo docker exec -it db_users sh
```

Acesse o _shell_ do mongo:

```bash
mongo
```

## Autenticando no banco de dados

Selecione o banco de dados e autentique-se no banco (Nota: lembre-se de utilizar o banco de dados, usuário e senha definidos no .env de seu repositório):     

```bash
use api_database
```

```bash
db.auth("api_user", "api_password")
```

Caso retorne "1", a autenticação foi realizada com sucesso.     

## Excluindo os usuários

Utilize o _find_ na _collection_ **_users_** para listar os usuários:

```bash
db.users.find()
```

Para excluir os usuários, é necessário selecionar a _collection_ **_users_** e então utilizar o _remove_:

```bash
db.users.remove({})
```

> Nota: este comando exclui todos os usuários, para excluir um usuário específico basta utilizar o _deleteOne_ enviando o _id_ do usuário obtido no comando do _find_:

```bash
db.users.deleteOne( {"_id": ObjectId("4d512b45cc9374271b02ec4f")});
```

Para sair do shell e do container, basta pressionar CTRL+C e depois CTRL+D.

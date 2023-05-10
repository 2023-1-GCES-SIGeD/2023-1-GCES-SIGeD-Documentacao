# Entrando no ambiente v2

## Introdução

Este guia tem como objetivo auxiliar novos desenvolvedores a entrarem pela primeira vez na aplicação completa localmente, trazendo o passo a passo para adicionar um login no sistema. 

Será necessário o [Docker](https://www.docker.com/products/docker-desktop/) e um software para se comunicar com APIs. Para este tutorial utilizamos o [Postman](https://www.postman.com/downloads/).

### Parte 1

Faremos pequenas mudanças no arquivo "routes.js" 
O caminho é:

```
2021-2-SiGeD-Users -> src -> routes.js
```
Dentro de routes.js você apagará " verify verify.JWT," das rotas GET/users (***linha 11***) e PUT/change-password/:id (***linha 15***). Neste momento seu código da routes.js deve ficar assim:

```JS
const express = require('express');
const verify = require('./Utils/functionsJWT');

const routes = express.Router();

const UserController = require('./Controllers/UserController');
const { verifyJWT } = require('./Utils/functionsJWT');

routes.get('/users/newest-four', verify.verifyJWT, UserController.newestFourUsersGet);
routes.get('/users/:id', verifyJWT, UserController.getSingleUser);
routes.get('/users', UserController.getAllUsers);
routes.post('/signup', UserController.createUser);
routes.post('/login', UserController.login);
routes.post('/recover-password', UserController.recoverPassword);
routes.put('/change-password/:id', UserController.changePassword);
routes.put('/users/update/:id', verify.verifyJWT, UserController.updateUser);
routes.delete('/users/delete/:id', verify.verifyJWT, UserController.toggleUser);

module.exports = routes;
```

### Parte 2
Agora, é necessário subir **somente** a pasta *2021-2-SiGeD-Users*, utilizando os seguintes comandos dentro dela:

```
docker network create siged_backend
```
```
docker-compose up    //tente "sudo" se der errado!
```

### Parte 3
Utilize o link <a href="http://localhost:3001/signup">http://localhost:3001/signup</a> na ferramenta `postman` e utilize o corpo em JSON abaixo e o verbo POST para cadastrar o novo usuário
Para adicionar JSON basta clicar em BODY -> raw e selecionar JSON.

>POST

```JSON
{
    "name": "Nome do Admin",
    "email": "seu.email.aqui@gmail.com",
    "role": "admin",
    "sector": "someSector",
    "pass": "Password@123"
}
```
*Modifique os campos `name:`, `email:` e `pass:`.*

Agora utilize o link [http://localhost:3001/users]() com o verbo GET e busque seus dados, lembrando que se o verify.JWT não for apagado o método vai retornar token invalido. Quando encontrar seus dados copie o seu ID.

Com seu ID em mãos você agora vai utilizar o link [http://localhost:3001/change-password/"seu id aqui"]() com o verbo PUT e colocar o seguinte JSON no BODY

>PUT

```JSON
{
    "pass": "Sua Senha permanente aqui"
}
```
*Modifique o campo `pass:`.*

Pronto agora sua nova senha foi cadastrada é você já é capaz de subir todos os containers e fazer login. Mas para ter certeza use o link [http://localhost:3001/login]() com seguinte corpo JSON no verbo POST.
>POST
```JSON
{
    "email": "Seu email"
    "pass": "Sua senha"
}
```
*Modifique os campos `pass:` e `email:`.*

Voilà, se tudo foi feito nos conformes você finalmente pode fazer login sem nenhum problema de email.

### LEMBRE-SE 
Depois de feito tudo, por favor lembre de retornar os "verify.JWT" eles são necessários para outras funções, e como sua senha já foi inserida eles não irão ser problemas depois do login.

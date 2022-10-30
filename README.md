<h1 align="center">
  Onlypets - API
</h1>

Esta é a documentação da fakeAPI utilizada no projeto front-end. A temática do projeto gira em torno de um site de adoções, avisos de animais perdidos e denuncias de maus tratos.

<br>

# Endpoints

O JSON para utilizar no Insomnia é este aqui -> https://drive.google.com/file/d/19YQ8giNmu3o32VsTGdwJ3Pr-tnl-mS0b/view?usp=sharing
Para importar o JSON no Insomnia é só baixar o arquivo. Na palavra "Insomnia" no canto superior esquerdo. Nesse dropdown é só clicar em "Import / Export > Import Data > From File" e selecionar o arquivo que foi feito download.

<br>
<br>

# Rotas que não precisam de autenticação

## Cadastro

**POST** /register <br/>
**POST** /signup <br/>
**POST** /users

Formato básico e obrigatório da requisição:

```json
{
  "email": "email@mail.com",
  "password": "1234"
}
```

<br>
Resposta:
 
```json
201 Created
{
  "accessToken": "xxx.xxx.xxx"
}
```

Você pode ficar a vontade para adicionar qualquer outra propriedade no corpo do cadastro dos usuários.
<br>
<br>

## Login

**POST** /login <br/>
**POST** /signin

Qualquer um desses 2 endpoints pode ser usado para realizar login com um dos usuários cadastrados na lista de "Users"

Formato da requisição:

```json
{
  "email": "email@mail.com",
  "password": "1234"
}
```

Resposta:

```json
200 OK
{
  "accessToken": "xxx.xxx.xxx"
}
```

<br>
<br>

## Pets

**GET** /pets <br>
Traz todos os pets cadastrados na aplicação aplicação

Resposta:

```json
200 Ok
[
  {
    "userId": "1",
	  "title": "nome do pet",
	  "content": "animal busca lar amoroso...",
	  "contact": "contato",
	  "temperament": "temperamento do pet",
	  "size": "tamanho do pet",
	  "age": "idade do pet",
	  "type" : "cão ou gato",
	  "city": "animal está para adoção onde?",
    "id": 1
  },
  {
    "userId": "1",
	  "title": "outro nome do pet",
	  "content": "outro animal busca lar amoroso...",
	  "contact": "outro contato",
	  "temperament": "temperamento do pet",
	  "size": "tamanho do pet",
	  "age": "idade do pet",
	  "type" : "cão ou gato",
	  "city": "animal está para adoção onde?",
    "id": 2
  },
];
```

<br>
<br>

# Rotas que necessitam de autorização

Rotas protegidas. Devem vir acompanhadas de um header com o token da seguinte forma:

```json
{
  "Authorization": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Implc3NpY2FAbWFpbC5jb20iLCJpYXQiOjE2NjY4MzA0NzMsImV4cCI6MTY2NjgzNDA3Mywic3ViIjoiMiJ9.u3Hyez-wNP6s8pcsEYn2d9kzAnVZWv9zFyABPxG7vv4"
}
```

<br>

## Usuários

**GET** /users/:userId <br>
Retorna o perfil do usuário logado

Resposta:

```json
200 OK
{
	"email": "kenzinho@mail.com",
	"password": "$2a$10$fe9..KCGT8QRPN53jqJ9KeW5GCNafxLxQOTRx5KccRJoCLa1d93Za",
	"id": 1,
	"contact": "contato do usuário",
	"adress": "enderreço do usuário",
	"preferences": {
		"temperament": "temperamento do pet",
		"size": "tamanho do pet",
		"age": "idade do pet",
		"type": "cão ou gato",
		"city": "animal está para adoção onde?"
	}
}
//usuário completo

||

200 OK
{
  "email": "kenzinho@mail.com",
	"password": "$2a$10$fe9..KCGT8QRPN53jqJ9KeW5GCNafxLxQOTRx5KccRJoCLa1d93Za",
	"id": 1,
}
//usuário inicial

```

<br>

**PATCH** /user <br>
Edita informação da publicação de adoção. <br>

Formato da Request - deve conter todas as informações a serem atualizadas:

```json
{
  "contact": "contato do usuário",
  "adress": "enderreço do usuário",
  "preferences": {
    "temperament": "temperamento do pet",
    "size": "tamanho do pet",
    "age": "idade do pet",
    "type": "cão ou gato",
    "city": "animal está para adoção onde?"
  }
}
```

userId deve ser o identificador do usuário logado.

Resposta:

```json
200 OK
{
	"email": "kenzinho@mail.com",
	"password": "$2a$10$fe9..KCGT8QRPN53jqJ9KeW5GCNafxLxQOTRx5KccRJoCLa1d93Za",
	"id": 1,
	"contact": "contato do usuário",
	"adress": "enderreço do usuário",
	"preferences": {
		"temperament": "temperamento do pet",
		"size": "tamanho do pet",
		"age": "idade do pet",
		"type": "cão ou gato",
		"city": "animal está para adoção onde?"
	}
}
```

<br>

**DELETE** /users/:userId<br>
Deleta o perfil do usuário logado

Resposta:

```json
200 OK
```

<br>

## Pets

**POST** /pets <br>
Cria uma nova publicação de adoção. <br>

Formato da Request:

```json
{
  "userId": "1",
  "title": "nome do pet",
  "content": "animal busca lar amoroso...",
  "contact": "contato",
  "temperament": "temperamento do pet",
  "size": "tamanho do pet",
  "age": "idade do pet",
  "type": "cão ou gato",
  "city": "animal está para adoção onde?"
}
```

userId deve ser o identificador do usuário logado.

Resposta:

```json
201 Created
{
  "userId": "1",
	"title": "nome do pet",
	"content": "animal busca lar amoroso...",
	"contact": "contato",
	"temperament": "temperamento do pet",
  "size": "tamanho do pet",
  "age": "idade do pet",
  "type" : "cão ou gato",
  "city": "animal está para adoção onde?",
  "id": 1
}
```

<br>

**PATCH** /pets/:postPetId <br>
Edita informação da publicação de adoção. postPetId é o identificador do post a ser editado.
<br>

Formato da Request - deve conter todas as informações a serem atualizadas:

```json
{
  "title": "novo titulo",
  "content": "novo conteúdo do post"
  ...
}
```

Resposta:

```json
200 OK
{
  "userId": "3",
  "title": "novo titulo do post",
  "content": "novo conteúdo do post",
  ...
  "id": 1
}
```

<br>

**DELETE** /pets/:postPetId <br>
Deleta a publicação de adoção. postPetId é o identificador do post a ser deletado.

Resposta:

```json
200 OK
```

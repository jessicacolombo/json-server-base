<h1 align="center">
  Onlypets - API
</h1>

Esta é a documentação da fakeAPI utilizada no projeto front-end. A temática do projeto gira em torno de um site de adoções, avisos de animais perdidos e denuncias de maus tratos.

URL base: <a> https://onlypetz.herokuapp.com/ </a>

<br>

# Endpoints

O JSON para utilizar no Insomnia é este aqui -> https://drive.google.com/file/d/10oTxTUMb00Im-Oov_trhI5eQr2VAO1XV/view?usp=sharing
Para importar o JSON no Insomnia é só baixar o arquivo. Na palavra "Insomnia" no canto superior esquerdo. Nesse dropdown é só clicar em "Import / Export > Import Data > From File" e selecionar o arquivo que foi feito download.

<br>
<br>

# Rotas que não precisam de autenticação

## Cadastro

**POST** /register <br/>

Formato da requisição:

```json
{
  "email": "email@mail.com",
  "password": "1234",
  "shelter": "false"
}
```

Resposta:

```json
201 Created
{
  "accessToken": "........",
	"user": {
		"email": "email@mail.com",
		"shelter": "false",
		"id": 1
}
```

<br>

## Login

**POST** /login <br>

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
    "castrated": "é castrado?",
    "vaccinated": "é vacinado?",
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
    "castrated": "é castrado?",
    "vaccinated": "é vacinado?",
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

**GET** /users <br>
Retorna todos os usuários (abrigos e normais) cadastrados.

```json
200 OK
[
    {
      "email": "kenzinho@mail.com",
      "password": "$2a$10$fe9..KCGT8QRPN53jqJ9KeW5GCNafxLxQOTRx5KccRJoCLa1d93Za",
      "id": 1,
      "shelter": "false"
    },
    {
      "email": "teste@mail.com",
      "password": "$2a$10$8U2fIrtlUHatMYZLdXFsHOCqsglyE3JJRASRiM5DHdcfJTBuOlh1G",
      "shelter": "false",
      "id": 2
    }
];

```

<br>

**GET** /users/:userId <br>
Retorna o perfil do usuário.

Resposta:

```json
200 OK
{
  "email": "kenzinho@mail.com",
  "password": "$2a$10$fe9..KCGT8QRPN53jqJ9KeW5GCNafxLxQOTRx5KccRJoCLa1d93Za",
  "shelter": "false",
  "id": 1,
  ...
}
```

<br>

**PATCH** /users/:userId <br>
Edita informação do perfil do usuário. userId deve ser o identificador do usuário logado - o usuário deve ser o dono do recurso para poder editá-lo. <br>

Formato da Request - deve conter todas as informações a serem atualizadas:

```json
{
  "imgProfile": "url ou permitir que faça upload",
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
Deleta o perfil do usuário logado. userId deve ser o identificador do usuário logado - o usuário deve ser o dono do recurso para poder editá-lo. <br>

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
  "title": "nome do pet",
  "content": "animal busca lar amoroso...",
  "contact": "contato",
  "temperament": "temperamento do pet",
  "size": "tamanho do pet",
  "age": "idade do pet",
  "type": "cão ou gato",
  "city": "animal está para adoção onde?",
  "castrated": "é castrado?",
  "vaccinated": "é vacinado?"
}
```

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
  "castrated": "é castrado?",
  "vaccinated": "é vacinado?",
  "id": 1
}
```

<br>

**PATCH** /pets/:postPetId <br>
Edita informação da publicação de adoção. postPetId é o identificador do post a ser editado - o usuário deve ser o dono do recurso para poder editá-lo. <br>.
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

## Denúncias

**GET** /reports <br>
Traz todas as denúncias de maus tratos cadastradas na aplicação.

Resposta:

```json
200 Ok
[
  {
    "userId": "1",
	  "title": "denuncia",
	  "description": "descrição do fato ocorrido",
	  "adress": "onde aconteceu?",
    "id": 1
  },
];
```

<br>
**POST** /reports <br>
Cadastra uma nova denuncia. <br>

Formato da Request:

```json
{
  "userId": "1",
  "title": "denuncia",
  "description": "descrição do fato ocorrido",
  "adress": "onde aconteceu?"
}
```

userId é a identificação do usuário que está criando a denuncia.

Resposta:

```json
201 Created
{
  "userId": "1",
  "title": "denuncia",
	"description": "descrição do fato ocorrido",
  "adress": "onde aconteceu?",
  "id": "1"
}
```

<br>

**PATCH** /reports/:reportId <br>
Edita informação da denuncia. reportId é o identificador da denuncia a ser editada - o usuário precisa ser o dono do recurso para poder editá-lo.
<br>

Formato da Request - deve conter todas as informações a serem atualizadas:

```json
{
  "title": "novo titulo da denuncia",
	"description": "nova descrição do fato ocorrido",
  ...
}
```

Resposta:

```json
200 OK
{
  "userId": "1",
  "title": "novo titulo da denuncia",
	"description": "nova descrição do fato ocorrido",
  ...
  "id": 1
}
```

<br>

**DELETE** /reports/:reportId <br>
Deleta a denuncia. reportId é o identificador da denuncia a ser editada - o usuário precisa ser o dono do recurso para poder deletá-lo.

Resposta:

```json
200 OK
```

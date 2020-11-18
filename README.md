<h1 align="center">
  <img alt="GymZone" title="GymZone" src=".github/logo.png" width="200px" />
</h1>

<h3 align="center">
  GymZone
</h3>

<h4 align="center">
  Gerenciando sua Academia
</h4>

## :zap: A aplicação

API Rest feita com Node.js para gerenciamento de academia.

### Um pouco sobre as ferramentas

Utiliza [Express](https://expressjs.com/) com as seguintes ferramentas:

- Sucrase + Nodemon;
- ESLint + Prettier + EditorConfig;
- Sequelize (integração com PostgreSQL ou MySQL);

### Funcionalidades

Abaixo estão as funcionalidades da aplicação.

#### 1. Autenticação

Permite que um usuário se autentique na aplicação utilizando e-mail e senha.

A autenticação é realizada utilizando JWT. Os dados de entrada são validados a ferramenta YUP.

Também permite a criação de usuário administrador utilizando a funcionalidade de [seeds do sequelize](https://sequelize.org/master/manual/migrations.html#creating-first-seed), essa funcionalidade tem o propósito de criação de registros na base de dados de forma automatizada.

Para criar um seed use o seguinte comando:

```js
yarn sequelize seed:generate --name admin-user
```

No arquivo gerado na pasta `src/database/seeds`, basta adicionar o código referente à criação de um usuário administrador:

```js
const bcrypt = require("bcryptjs");

module.exports = {
  up: QueryInterface => {
    return QueryInterface.bulkInsert(
      "users",
      [
        {
          name: "Admin",
          email: "admin@gymzone.com",
          password_hash: bcrypt.hashSync("12345678", 8),
          created_at: new Date(),
          updated_at: new Date()
        }
      ],
      {}
    );
  },

  down: () => {}
};
```

Depois execute:

```js
yarn sequelize db:seed:all
```

#### 2. Cadastro de alunos

- Os alunos podem ser mantidos (cadastrados/atualizados) na aplicação utilizando nome, email, idade, peso e altura.

- Uma tabela chamada `students` é usada no banco de dados.

- Administradores são os únicos com senha, ou seja, alunos não podem se autenticar no sistema.

- O cadastro de alunos só pode ser realizado por administradores autenticados na aplicação.
---

Feito com ♥ by YuriRibeiro

# Passos para criar API em Node.js

Duas opções:

A mais fácil: Você pode clonar esse repositório e rodar

> yarn install

A mais legal: Seguir o passo a passo abaixo

### estrutura

##### pastas

- src
- src/app
- src/app/controllers
- src/app/models
- src/config
- src/database
- src/database/migrations

##### arquivos

- src/app.js
- src/server.js
- src/routes.js
- src/config/database.js

### comandos iniciais

- yarn init -y
- yarn add express
- yarn add sucrase nodemon -D
- yarn add eslint -D
- yarn add sequelize -D
- yarn add sequelize-cli -D
- yarn add pg pg-hstore
- yarn add bcryptjs _(opcional para aplicar hash em senhas)_
- yarn add jsonwebtoken _(opcional para trabalhar com autenticação JWT)_

### package.json

Adicionar:

```
"scripts" : {
  "dev" : "nodemon src/server.js"
},
```

### nodemon

Criar arquivo **nodemon.json** na raiz do projeto

```
{
  "execMap" : {
    "js" : "sucrase-node"
  }
}
```

### eslint

_Requer extensão ESLint (dbaeumer.vscode-eslint) instalada no VSCode_

> yarn eslint --init

Selecionar as seguintes opções:

- To check syntax, find problems, and enforce code style
- Javascript modules (import/export)
- None of These
- [ ] Browser
- [x] Node
- Use a popular style guide
- Airbnb
- Javascript
- Y

Deletar arquivo package-lock.json e atualizar dependencias do yarn com o comando:

> yarn

**Open Settings (JSON) - VSCode (CTRL+Shift+P)**

Adicionar:

```
"editor.formatOnSave": true,
"eslint.autoFixOnSave": true,
"eslint.validate": [
  {
    "language": "javascript",
    "autoFix": true
  },
  {
    "language": "javascriptreact",
    "autoFix": true
  },
  {
    "language": "typescript",
    "autoFix": true
  },
  {
    "language": "typescriptreact",
    "autoFix": true
  }
]
```

**.eslintrc.js**

Adicionar:

```
rules: {
  'prettier/prettier': 'error',
  'class-methods-use-this': 'off',
  'no-param-reassign': 'off',
  camelcase: 'off',
  'no-unused-vars': ['error', { argsIgnorePattern: 'next' }],
},
```

### prettier

Executar comando:

> yarn add prettier eslint-config-prettier eslint-plugin-prettier -D

**.eslintrc.js**

Alterar:

```
extends: ['airbnb-base', 'prettier'],
plugins: ['prettier'],
```

Criar arquivo **.prettierrc** na raiz do projeto

Contendo:

```
{
  "singleQuote": true,
  "trailingComma": "es5"
}
```

Dica: para realizar fix automatico em todos arquivos JS da pasta SRC:

> yarn eslint --fix src --ext .js

### editorconfig

_Requer extensão EditorConfig (editorconfig.editorconfig) instalada no VSCode_

Criar arquivo **.editorconfig** na raiz do projeto (ou clicar com botão direito do mouse em cima da pasta do projeto no VSCode e selecionar a opção 'Generate .editorconfig)

Criar ou alterar com:

```
root = true

[*]
indent_style = space
indent_size = 2
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

### sequelize

Criar arquivo **.sequelizerc** na raiz do projeto.

Contendo:

```
const { resolve } = require('path');

module.exports = {
  config: resolve(__dirname, 'src', 'config', 'database.js'),
  'models-path': resolve(__dirname, 'src', 'app', 'models'),
  'migrations-path': resolve(__dirname, 'src', 'database', 'migrations'),
  'seeds-path': resolve(__dirname, 'src', 'database', 'seeds'),
};
```

Configure o arquivo **src/config/database.js**

```
module.exports = {
  dialect: '<tipo de banco, ex: postgres, mysql>',
  host: '<host, ex: localhost>',
  username: '<seu username>',
  password: '<sua senha>',
  database: '<seu banco de dados>',
  define: {
    timestamps: true,
    undescored: true,
    undescoredAll: true,
  },
};
```

### Isso é tudo pessoal!

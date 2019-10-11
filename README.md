# MeetAppWerner

## Comandos Usados

Para inicializar o package.json na pasta:<br>
`yarn init`

Adcionando o Express: <br>
`yarn add express`

Para executar o servidor no estado Atual:<br>
`yarn dev`

Para adcionar as novas funcionalidades de import no node usaremos o sucrase.
Para visualizar mudancas nos arquivos e atualizar o servidor usamos o nodemon para tornar o desenvolvimento mais rapido:<br>
`yarn add sucrase nodemon`

Para executar o sucrase manualmente pode usar:<br>
`yarn sucrase-node [caminhodoarquivo]`

Para usar o nodemon temos que criar no package.json o seguinte parametro de scripts abaixo de license:

```JSON
{
  "license": "MIT",
  "scripts": {
    "dev":"nodemon src/server.js"
  }
}
```

Porem e necessario tambem criar um arquivo de configuracao do nodemon para dizer que queremos que ele execute o sucrase-node inves do node puro.
<br><br>
Criando um arquivo chamado nodemon.json coloca-se o objeto abaixo:

```JSON
{
  "execMap": {
    "js":"sucrase-node"
  }
}
```

<br>

## Usando Docker e o Configurando

O docker e uma ferramenta usada para isolamento de ambientes de desenvolvimento, como bancos de dados, Sistemas Operacionais entre outros.<br>
Esse isolamento e chamado de Container.<br>
Imagem eh um servico disponivel pelo docker
<br>
O container eh uma instancia de uma imagem.
<br> Os registros dessas dependencias sao encontradas no Docker Registry.

Para sabser se o docker esta na maquina:
`docker help`

Para instalar um container postgres usa-se:<br>
`docker run --name meetappdb -e POSTGRES_PASSWORD=docker -p 5433:5432 -d postgres`

Onde:<br>
`POSTGRESS_PASSWORD=` Define a senha do postgres<br>
`-p 5433:5432` Define a porta de entrada e saida, no caso estao diferentes pois minha maquina ja possui o postgres instalado. <br>
`-d postgres` Define a Imagem usada.<br>

Para saber quais containers estao rodando:<br>
`docker ps`

Para ver todos os containers:<br>
`docker ps -a`

para iniciar o container: <br>
`docker start [nomedocontainer]`

para ver os logs:<br>
`docker logs [nomedocontainer]`

## Configurando o Sequelize

### ORM

O sequelize eh um ORM.<br>
Um ORM eh um meio de abstrair o banco de dados.<br>
No Banco de dados possui tabelas, no ORM Viram models<br>
A manipulacao dos dados eh feito sem SQL na maioria das vezes, apenas javascript.<br><br>

### Migration

Existe uma funcionalidade chamada Migration que funciona como um meio de ter controle de versoes para base de dados.<br>
Cada Arquivo contem instrucoes para criacao alteracao ou remocao de tabelas e colunas <br>
Cada arquivo eh uma migration e sua ordenacao ocorre por Data;<br>
Cada migration cria apenas uma tabela.

### Seeds

Outra funcionalidade eh a Seeds<br>
Sao arquivos que populam dados para desenvolvimento<br>
Muito usados para testes<br>
Executavel apenas por comandos<br>
Jamais sera usado em producao<br>

## Arquitetura MVC

A forma de estruturacao dessa Aplicacao

### Model

Armazena a abstracao do banco. Nao possui responsabilidade de regra de negocio.

### Controller

Ponto de entrada das requisicoes da Aplicacao, uma rota geralmente esta associada diretamente com um metodo controller. Pode-se incluir grande parte das regras de negocio da aplicacao nos controllers(conforme a aplicacao cresce podemos isolar as regras)

### View

Eh o retorno ao cliente, em aplicacoes que nao estao utilizando modelo de API REST isso pode ser um HTML, mas no caso do MeetApp a view eh apenas nosso JSON que sera retornado ao front-end e depois manipulado pelo ReactJS ou React Native

## ESlint, Prettier & EditorConfig

Sao Utilizados para criar um padrao de escrita de codigo entre varios Devs.<br>
Adicionamos o Eslint como dependencia de desenvolvimento:<br>
`yarn add eslint -D`<br>
Depois iniciamos ele:<br>
`yarn eslint --init`<br>
Apos isso apague o package-lock criado, e rode um `yarn` na pasta do projeto.<br>
Nesse processo foi gerado um arquivo chamado ".eslintrc.js" eh onde ficaram as configuracoes dele.<br>
No vscode eh necessario baixar o complemento.<br>
Para fazer o ESlint fazer o fix automatico eh necessario passar algumas configs para o arquivo de configuracao do vscode.<br>

```JSON
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
    },
  ],
```

<br>Iremos sobreescrever algumas regras do eslintrc:<br>

```javascript
module.exports = {
  env: {
    es6: true,
    node: true,
  },
  extends: ['airbnb-base'],
  globals: {
    Atomics: 'readonly',
    SharedArrayBuffer: 'readonly',
  },
  parserOptions: {
    ecmaVersion: 2018,
    sourceType: 'module',
  },
  rules: {
    'class-methods-use-this': 'off',
    'no-param-reassign': 'off',
    camelcase: 'off',
    'no-unused-vars': ['error', { argsIgnorePattern: 'next' }],
  },
};
```

<br>

Adicionamos tambem o Prettier com os complementos para rodar junto do eslint.
Como dependencia de Desenvolvimento.
`yarn add prettier eslint-config-prettier eslint-plugin-prettier -D`<br>
e depois disse mudamos o eslintrc novamente.<br>

```javascript
module.exports = {
  env: {
    es6: true,
    node: true,
  },
  extends: ['airbnb-base', 'prettier'],
  plugins: ['prettier'],
  globals: {
    Atomics: 'readonly',
    SharedArrayBuffer: 'readonly',
  },
  parserOptions: {
    ecmaVersion: 2018,
    sourceType: 'module',
  },
  rules: {
    'prettier/prettier': 'error',
    'class-methods-use-this': 'off',
    'no-param-reassign': 'off',
    camelcase: 'off',
    'no-unused-vars': ['error', { argsIgnorePattern: 'next' }],
  },
};
```

<br>
Precisamos editar tambem algumas regras que se sobrepoe.
<br>No arquivo .prettierrc:

```JSON
{
  "singleQuote": true,
  "trailingComma": "es5"
}
```

<br> Para fixar varios arquivos de uma vez usando eslint apenas usamos o comando:<br>

`yarn eslint --fix pasta --ext .js`

<br>
A ultima ferramenta eh o EditorConfig que eh um modulo do vscode.
<br>
criamos um arquivo chamado .editorconfig no menu disponivel na raiz do projeto com o botao direito.
<br> Essa eh a configuracao do meu:

```
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

```

Se o seu se parece com este apenas mude as 2 ultimas instrucoes para true.
<br>

## Configurando o Sequelize

### Configuracao de Pastas

Dentro da pasta `./src` criada anteriormente, criaremos uma pasta chamada `./config` <br>
e dentro dessa pasta colocaremos as configuracoes de conexao com banco de dados em um arquivo chamado
`database.js` <br>
Ainda dentro da pasta `./src` criaremos uma pasta chamada `./database` e dentro dela a pasta `./migrations` onde ficaram as configuracoes de criacao de tabelas no banco de dados.
<br>
Na Pasta `./src` criaremos uma pasta chamada `./app` onde ficarao todos codigos de regra de negocio.<br>
Em seguida dentro da pasta `./app` criaremos as pastas `./model` e `./controller`.

### Instalacao do Sequelize

No terminal iremos digitar os comandos: <br>
`yarn add sequelize`: para adicionar o sequelize ao projeto. <br>
`yarn add sequelize-cli -D`: para adicionar a ferramenta executavel do sequelize como dependencia de desenvolvimento.<br>

Criaremos um arquivo na raiz do projeto com o nome `.sequelizerc` que eh onde poderemos "exportar" os caminhos dos arquivos de configuracao de conexao e de criacao de migrations.<br>
Neste arquivo apenas podemos utilizar a sintaxe de importacao do CommomJS (require).
<br>

O arquivo de se parecer com isso:

```javascript
const { resolve } = require('path');

module.exports = {
  config: resolve(__dirname, 'src', 'config', 'database.js'),
  'models-path': resolve(__dirname, 'src', 'app', 'models'),
  'migrations-path': resolve(__dirname, 'src', 'database', 'migrations'),
  'seeders-path': resolve(__dirname, 'src', 'database', 'seeds'),
};
```

<br>

Apos isso, configuraremos o arquivo `./src/config/database.js`.<br>
Para configuracao do dialeto do banco de dados postgres, precisamos instalar estas dependencias:
`yarn add pg pg-hstore`. <br>

Se voce seguiu as instrucoes corretamente ate aqui, seu arquivo de database deve estar semelhante a isso: <br>

```javascript
module.exports = {
  dialect: 'postgres',
  host: 'localhost',
  username: 'postgres',
  password: 'docker',
  database: 'meetapp',
  define: {
    timestamps: true,
    underscored: true,
    underscoredAll: true,
  },
};
```

<br>
As regras de timestamps sao para mostrar quando um registro foi alterado, underscored e underscoredAll sao para enforcar que as tabelas criadas sejam criadas nome_da_tabela e nao NomeDaTabela.
<br>

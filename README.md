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

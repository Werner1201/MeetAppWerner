# MeetAppWerner

## Comandos Usados
Para inicializar o package.json na pasta:<br>
```yarn init```

Adcionando o Express: <br>
```yarn add express```

Para executar o servidor no estado Atual:<br>
```yarn dev```

Para adcionar as novas funcionalidades de import no node usaremos o sucrase.
Para visualizar mudancas nos arquivos e atualizar o servidor usamos o nodemon para tornar o desenvolvimento mais rapido:<br>
```yarn add sucrase nodemon```

Para executar o sucrase manualmente pode usar:<br>
```yarn sucrase-node [caminhodoarquivo]```

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


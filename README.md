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
<br>

## Usando Docker e o Configurando
O docker e uma ferramenta usada para isolamento de ambientes de desenvolvimento, como bancos de dados, Sistemas Operacionais entre outros.<br>
Esse isolamento e chamado de Container.<br>
Imagem eh um servico disponivel pelo docker
<br>
O container eh uma instancia de uma imagem.
<br> Os registros dessas dependencias sao encontradas no Docker Registry.

Para sabser se o docker esta na maquina:
``` docker help ```

Para instalar um container postgres usa-se:<br> 
```docker run --name meetappdb -e POSTGRES_PASSWORD=docker -p 5433:5432 -d postgres```

Onde:<br> 
```POSTGRESS_PASSWORD= ``` Define a senha do postgres<br>
```-p 5433:5432 ``` Define a porta de entrada e saida, no caso estao diferentes pois minha maquina ja possui o postgres instalado. <br>
```-d postgres ``` Define a Imagem usada.

Para saber quais containers estao rodando:
```docker ps```

Para ver todos os containers:
```docker ps -a ```

para iniciar o container: 
```docker start [nomedocontainer]```

para ver os logs:
``` docker logs [nomedocontainer]```



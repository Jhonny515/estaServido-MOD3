# Estão Servidos? - Projeto Individual Módulo 3 

<img src="./assets/img/Resilia_RD.png" style="margin: 0 10%; width: 80%">

<span style="font-size: smaller">

**Feito por:** Jonatas (Jhonny) <br>
**Linguagens utilizadas:** JSON <br>
**Tecnologias utilizadas:** json-server, node.js, postman.com, axios, javascript

</span>

Projeto Resilia onde devemos desenvolver uma fake API com dados mokados, utilizando o pacote *'json-server'* para criar um servidor de teste. O servidor deverá  conter ao menos 2 rotas com 3 ou mais dados, nas quais o usuário poderá realizar os métodos <span style="background: #ffd; color: #3b3b38;">GET</span>, <span style="background: #ffd; color: #3b3b38;">POST</span>, <span style="background: #ffd; color: #3b3b38;">PUT</span> e <span style="background: #ffd; color: #3b3b38;">DELETE</span>.

## Índice
* [Tema do "db.json"](#tema-do-dbjson)
* Como executar o servidor
    * [JSON-SERVER](#json-server)
    * [Requisições HTTP](#requisições-http)
        * [Utilizando POSTMAN](#utilizando-postman)
        * [Utilizando AXIOS](#utilizando-axios)
* [Links Úteis](#links-úteis)

## Tema do "db.json"

Para este projeto, tínhamos que desenvolver um servidor de dados que seria utilizado em nossas aulas. Nós poderíamos escolher o nicho no qual o nosso banco de dados se basearia. Eu escolhi o tema **"música"**.

Este banco de dados possui 3(três) rotas: 
- Artista
- Album
- Música

Na rota artista, os dados são o nome do artista e os álbuns que ele possui, além do identificador **ID**, necessário para identificação do json-server.

Na rota album, cada álbum possui nome, tipo, data de lançamento e lista de faixas, além do identificador. Esta rota também possui identificadores relacionais, como o ID do artista, e lista de faixas utiliza o ID das faixas em *array*. O ID do albúm também relaciona o albúm ao artista, utilizando um padrão de escrita:

| ID do Artista | - | ID do Álbum |
|:---:|:---:|:---:|
| 1 | - | 1 |

Na rota de música, além do nome da música e do gênero, temos os identificadores da música, do albúm ao qual pertence e do artista. O ID da música segue o padrão relacional do álbum, unindo o id do artista, do álbum e agora da música, separados por hífen:

| ID do Artista | - | ID do Álbum | - | ID da Música |
|:---:|:---:|:---:|:---:|:---:|
| 1 | - | 1 | - | 1 |

Os dados usados nesse server são **mokados**, significando que eles não são reais, seu uso sendo direcionado apenas para testes.

## Como executar o servidor

### JSON-SERVER

Este projeto foi desenvolvido para ser usado com o pacote do node.js *'json-server'*, sendo necessário possuir o ambiente node.js  instalado.

O *json-server* é uma biblioteca que permite criar uma Rest API (API de teste), de maneira rápida e sem código.

Para tal, inicialmente é necessário instalar o pacote do *json-server* via linha de comando, escrevendo no terminal de sua preferência:

`npm install -g json-server`

<span style="font-size: smaller">

\*O comando '-g' é opcional, e serve para instalar o pacote globalmente, possibilitando seu uso em todos os seus projetos com node. Sem esse comando, o pacote será instalado apenas localmente, podendo ser utilizado apenas no projeto em que foi instalado.

</span>

Após baixar o json-server, crie seu banco de dados em formato **json**. No caso, neste projeto ele já está criado, sendo necessário somente a instalação do json-server e sua utilização.

Para iniciar o servidor local para poder fazer uso dos dados em sua aplicação, digite na linha de comando o comando:

`json-server --watch db.json`

<span style="font-size: smaller">

\*Talvez seja necessário utilizar um executor de pacotes, caso sua máquina possua restrições na utilização de pacotes. Com o node.js, inclua no início da linha de comando: "npx" .

</span>

**"json-server"** chama a biblioteca para execução. **"--watch"** permite que as alterações no arquivo possam ser observadas e efetivadas. "**db.json**" é o nome do arquivo json que contém os dados que vamos utilizar. Caso esteja criando seu próprio arquivo com um nome diferente, coloque o nome do seu arquivo no lugar.

Com isso, o json-server criará as URLs para sua *Rest API*. Daí, é só utilizá-la em requisições HTTP.

<img src="./assets/img/Captura de tela TERMINAL_json-server.png" alt="Servidor local criado junto com as rotas">
<br> <br> <br>

### Requisições HTTP

Para poder pegar os dados, manipulá-los ou deletá-los em sua aplicação, será necessário utilizar **requisições HTTP**. 
>Requisições HTTP são mensagens enviadas pelo cliente para iniciar uma ação no servidor. <br>
<a href="https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Messages">(MDN web docs)</a>

As requisições mais comuns são: **GET** (permite acessar e visualizar os dados), **POST** (permite inserir novos dados), **PUT** (permite atualizar dados, ou como o método POST, inserir também) e **DELETE** (permite excluir dados).

Essas requisições podem ser feitas de diversas formas. Diretamente no código de sua aplicação ou utilizando ferramentas de desenvolvimento de API que forneçam uma ferramenta de *API Client*, como o **Postman.com**.

Este projeto foi testado utilizando o **Postman.com** e o pacote **AXIOS**, também pertencente ao node.js, e nos permite fazer requisições de API em nosso código de maneira mais rápida.

#### **Utilizando POSTMAN**

Acesse https://www.postman.com/ e faça seu cadastro, ou login se já for cadastrado.

Após isso, será necessário instalar o **Postman Agent** que permitirá que você utilize servidores locais (implementados em sua máquina).

Acesse a aba '*Workspaces*' e crie um novo workspace para começar a fazer suas requisições.

<img src="./assets/img/Captura de tela POSTMAN.png" alt="Workspace do POSTMAN">

Insira o URL do servidor do *json-server* no campo de endereço do Postman. À esquerda do campo, você pode escolher a requisição HTTP que deseja utilizar.

Para **GET**, use a rota que quer visualizar ou a rota/id do dado que quiser visualizar.

Para **POST**, use a rota onde quer incluir um novo dado e na aba "body", escreva o novo dado a ser incluído em objeto json. Utilize o modo de texto *"raw"* e tipo *"JSON"*.

<img src="./assets/img/Captura de tela POSTMAN_POST.png" alt="POSTMAN: exemplo do método POST">

Para **PUT**, use como POST para incluir um novo dado. Para atualizar um dado, insira na URL a rota/id do dado a ser atualizado e no body os campos a serem alterados.

Para **DELETE**, use a rota/id do dado que deseja exluir.

O *json-server* pode criar um ID automaticamente, incrementando a partir do último ID se o mesmo for numérico. Como as rotas "album" e "musica" utilizam IDs personalizados, não consegui encontrar a forma de o *json-server* automaticamente relacionar e criar os IDs. Ao menos não via Postman.

Para evitar strings aleatórias criadas pelo *json-server*, recomendo escrever os IDs de albuns e músicas, co-relacionando os dados.

Para a rota "artista", os IDs são numéricos, então você pode testar a funcionalidade de *autoincrement ID* nessa rota.
<br> <br>

#### **Utilizando AXIOS**

**AXIOS** é um pacote cliente HTTP baseado em *Promises*, permitindo fazer requisições HTML no browser e no node.js com a mesma base de código.

A sua instalação também é feita via terminal, utilizando o comando:

`npm install axios`

A sua utilização será feita diretamente no código, chamando o pacote via **require** no javascript ou **import** no React.js.

Sua sintaxe geralmente consiste em invocar o axios com o verbo de requisição, e passando a URL no argumento.

```javascript
const axios = require('axios');

// Fazendo uma requisição de um usuário com ID
axios.get('/user?ID=12345')
  .then(function (response) {
    // Tratando sucesso
    console.log(response);
  })
  .catch(function (error) {
    // Tratando erro
    console.log(error);
  })
  .then(function () {
    // Sempre executado
  });
  ```

O exemplo acima foi retirado da documentação do AXIOS. Para melhor entendimento e mais exemplos, deixarei o link da documentação como referência:

https://axios-http.com/ptbr/docs/intro

## Links úteis

  Site do *node.js*: <br>
  https://nodejs.org/pt-br/
  <br> <br>

  Página do *json-server* no site da *npm*: <br>
  https://www.npmjs.com/package/json-server
  <br> <br>

  Documentação do *AXIOS*: <br>
  https://axios-http.com/ptbr/docs/intro
  <br> <br>

  Site do *Postman*: <br>
  https://www.postman.com
# 🚀 Resumo — Aula 04: Consumindo APIs no Front-end

## 1. O que é uma API?

API (*Application Programming Interface* ou Interface de Programação de Aplicações) é um conjunto de protocolos, rotinas e ferramentas que define como diferentes componentes de software devem interagir.

Ela permite a comunicação entre sistemas distintos, mesmo quando eles utilizam linguagens, plataformas ou tecnologias diferentes.

### REST

REST (*Representational State Transfer*) é um estilo arquitetural utilizado principalmente no desenvolvimento de sistemas distribuídos na web.

Seus principais princípios são:

- Comunicação cliente-servidor sem estado (*stateless*);
- Uso dos métodos HTTP;
- Identificação dos recursos por URIs;
- Transferência de representações de dados, como JSON.

---

## 2. Protocolo HTTP

HTTP (*Hypertext Transfer Protocol*) é o protocolo responsável pela comunicação na World Wide Web. Ele define as regras para a troca de informações entre clientes, como navegadores, e servidores.

### Conceitos principais

- **Modelo cliente-servidor:** o front-end faz requisições e o servidor processa e responde;
- **Stateless:** cada requisição é independente, sem que o servidor precise lembrar das requisições anteriores;
- **Baseado em texto:** as mensagens HTTP podem ser lidas e analisadas por pessoas.

### Métodos HTTP

| Método | Finalidade | Característica |
|---|---|---|
| **GET** | Recuperar informações | Seguro e idempotente; não altera os dados |
| **POST** | Criar um recurso | Não idempotente; chamadas repetidas podem criar vários recursos |
| **PUT** | Substituir um recurso | Atualiza completamente os dados |
| **PATCH** | Atualizar um recurso | Altera apenas parte dos dados |
| **DELETE** | Remover um recurso | Idempotente; excluir novamente não deve causar alteração adicional |

---

## 3. Como funciona uma requisição

O fluxo básico entre uma aplicação e uma API ocorre da seguinte forma:

1. O usuário acessa uma página ou realiza uma ação no front-end;
2. O navegador envia uma requisição HTTP, como GET, POST, PUT ou DELETE;
3. O servidor recebe a requisição, identifica a rota e executa a lógica necessária;
4. O servidor consulta, grava ou atualiza informações em um banco de dados ou em uma API externa;
5. A resposta é enviada, geralmente no formato JSON;
6. O front-end interpreta a resposta e atualiza a interface para o usuário.

---

## 4. Endpoint

Um **endpoint** é uma URL específica que fornece acesso a um recurso ou funcionalidade de uma API. Ele representa o ponto de comunicação entre o cliente e o servidor.

Um mesmo endpoint pode responder de formas diferentes conforme o método HTTP utilizado:

- **GET:** consulta ou lista informações;
- **POST:** adiciona um novo recurso.

Também podem ser utilizados PUT, PATCH e DELETE para atualizar e remover recursos.

Catálogos de APIs públicas, como o [Free Public APIs](https://www.freepublicapis.com/), ajudam a encontrar serviços para estudar e desenvolver aplicações reais.

---

## 5. JSON

JSON (*JavaScript Object Notation*) é um formato leve para troca de dados. Ele é fácil de ler e escrever por pessoas e simples de interpretar e gerar por máquinas.

Seus dois tipos principais de estrutura são:

- **Objetos:** coleções de pares nome/valor;
- **Arrays:** listas ordenadas de valores.

Exemplo de objeto JSON:

```json
{
  "id": "USER-001",
  "nome": "Carlos Silva",
  "email": "carlos@example.com",
  "idade": 28,
  "ativo": true,
  "endereco": {
    "cidade": "São Paulo",
    "estado": "SP"
  },
  "interesses": ["tecnologia", "esportes"]
}
```

O JSON pode conter textos, números, valores booleanos, objetos, arrays e valores vazios.

---

## 6. Backend e Web Service

### Servidor backend

É o sistema responsável por processar requisições, gerenciar dados e fornecer respostas para clientes, como navegadores e aplicativos.

Suas principais funções são:

- Armazenar e recuperar dados;
- Executar regras de negócio;
- Fornecer APIs para a comunicação entre sistemas.

### Web Service

É um serviço acessível pela web que permite a comunicação entre sistemas por meio de HTTP ou HTTPS. Ele padroniza a troca de informações entre aplicações diferentes.

---

## 7. Criando uma API REST com Express

O **Express.js** é um framework minimalista e flexível para Node.js que facilita a criação de servidores web e APIs.

### Instalação

```bash
npm install express
npm install cors
```

### Exemplo de API

```javascript
import express from 'express';
import cors from 'cors';

const app = express();

app.use(cors());

app.get('/', (req, res) => {
  res.json({
    date: new Date().toLocaleString('pt-BR'),
    status: 'API funcionando!'
  });
});

const PORT = process.env.PORT || 3000;

app.listen(PORT, () => {
  console.log(`Servidor rodando na porta ${PORT}`);
});
```

Para iniciar o servidor:

```bash
node api.js
```

### CORS

CORS (*Cross-Origin Resource Sharing*) é um mecanismo de segurança do navegador que controla o acesso entre domínios diferentes. O middleware `cors()` permite que o front-end consuma a API quando estiver hospedado em uma origem diferente.

---

## 8. Recursos do Express.js

O Express simplifica o desenvolvimento com Node.js porque reduz a quantidade de código necessária para criar rotas e middlewares.

Principais recursos:

- **Roteamento:** definição de caminhos como `/users` e `/products`;
- **Middlewares:** funções que processam requisições e respostas, como autenticação, logs e tratamento de erros;
- **Leveza e velocidade:** adequado para criar APIs e servidores web rapidamente;
- **Integração:** facilita a comunicação com bancos de dados e outros serviços.

### Node.js puro e Express.js

No módulo `http` do Node.js, é necessário verificar manualmente a URL e controlar as respostas:

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  if (req.url === '/') {
    res.end('Olá, mundo!');
  } else {
    res.end('Rota não encontrada!');
  }
});

server.listen(3000);
```

Com Express, a definição da rota é mais direta:

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Olá, mundo!');
});

app.listen(3000);
```

### Quando utilizar

O Express é indicado para APIs REST, integração com bancos de dados, backends escaláveis, páginas com templates e aplicações que utilizam middlewares.

Para aplicações em tempo real, WebSockets podem ser mais adequados. Para processamento pesado, é preferível utilizar Workers.

---

## 9. Deploy com Render

O Render é uma plataforma de hospedagem em nuvem que suporta Node.js, Python e outras linguagens. Ele permite conectar um repositório GitHub e realizar deploy contínuo.

### Processo de publicação

1. Faça o commit do projeto em um repositório do GitHub;
2. Crie uma conta no [Render](https://dashboard.render.com/);
3. Crie um novo **Web Service** e conecte o repositório;
4. Configure o comando de build e o comando de inicialização;
5. Realize o deploy;
6. Acesse a API pelo endereço fornecido, como `seu-projeto.onrender.com`.

O Render oferece SSL, atualizações automáticas via GitHub, escalabilidade e monitoramento, sendo útil tanto para projetos acadêmicos quanto profissionais.

---

## 10. Atividades

### Atividade 01 — Pesquisa de APIs

Pesquisar 10 projetos no GitHub que utilizem APIs. Para cada projeto:

- Clonar e analisar o repositório;
- Identificar o framework utilizado;
- Identificar as APIs consumidas;
- Criar um arquivo Markdown com uma tabela contendo os projetos e suas informações.

### Atividade 02 — API de data e hora

1. Criar uma API com Express contendo uma rota para consulta de data e hora;
2. Fazer o deploy da API no Render a partir de um repositório GitHub;
3. Desenvolver uma aplicação front-end que consuma a API;
4. Exibir a data e a hora na tela;
5. Manter a API e o front-end em repositórios separados;
6. Organizar um documento com prints do código, da aplicação, dos painéis do Render e Vercel e inserir os links dos repositórios;
7. Enviar a atividade na plataforma Canva.

---

## ✅ Conclusão

Consumir APIs permite que aplicações front-end obtenham e enviem dados para outros sistemas. Para isso, é importante compreender o protocolo HTTP, seus métodos, endpoints e o formato JSON.

Com o Express.js, é possível criar uma API REST de forma simples e disponibilizá-la na nuvem com o Render. Assim, front-end e backend podem ser desenvolvidos separadamente e integrados por meio de requisições HTTP.

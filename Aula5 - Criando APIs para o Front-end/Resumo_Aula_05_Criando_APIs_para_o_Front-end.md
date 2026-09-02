# 🚀 Resumo — Aula 05: Criando APIs para o Front-end

## 1. Objetivos da aula

Nesta aula, o conteúdo sobre consumo de APIs é retomado e aplicado à criação de um back-end próprio. Os principais objetivos são:

- Compreender os métodos HTTP e suas finalidades;
- Identificar endpoints e estruturar dados em JSON;
- Diferenciar servidor back-end de Web Service;
- Criar uma API REST com Node.js e Express.js;
- Utilizar CORS para permitir a comunicação entre origens diferentes;
- Implementar um CRUD de notas com persistência em arquivo JSON;
- Publicar o back-end no Render e o front-end na Vercel.

---

## 2. Métodos HTTP

Os métodos HTTP indicam a operação que o cliente deseja realizar sobre um recurso da API.

| Método | Finalidade | Características |
|---|---|---|
| **GET** | Recuperar informações | É seguro e idempotente: várias chamadas não devem alterar os dados. |
| **POST** | Criar um novo recurso | Não é idempotente: chamadas repetidas podem criar vários recursos. |
| **PUT** | Substituir um recurso | Atualiza completamente os dados de um recurso existente. |
| **PATCH** | Atualizar um recurso parcialmente | Altera apenas os campos enviados. |
| **DELETE** | Remover um recurso | É idempotente: remover novamente algo que já não existe não deve produzir uma alteração adicional. |

### Idempotência

Uma operação é idempotente quando sua repetição produz o mesmo efeito final da primeira execução. Por exemplo, uma requisição `GET` apenas consulta dados, enquanto uma requisição `POST` repetida pode criar registros duplicados.

---

## 3. Endpoint

Um **endpoint** é uma URL específica que fornece acesso a um recurso ou funcionalidade de uma API. Ele representa o ponto de comunicação entre cliente e servidor.

Exemplo de referência:

- [Awesome API Brasil](https://github.com/awesomeapibrasil/awesomeapi-cep)

O comportamento de uma URL pode variar conforme o método HTTP utilizado. Em uma rota `/users`, por exemplo:

- `GET /users`: lista usuários;
- `POST /users`: adiciona um usuário;
- `PUT /users/:id`: substitui um usuário;
- `PATCH /users/:id`: altera parte de um usuário;
- `DELETE /users/:id`: remove um usuário.

O trecho `:id` é um parâmetro de rota usado para identificar um recurso específico.

---

## 4. JSON

JSON (*JavaScript Object Notation*) é um formato leve para troca de dados entre aplicações. Ele é legível por pessoas e facilmente interpretado e gerado por máquinas.

Os dois formatos estruturais principais são:

- **Objeto:** coleção de pares `nome: valor`;
- **Array:** lista ordenada de valores.

O JSON pode representar textos, números, valores booleanos, objetos, arrays e valores nulos.

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

Exemplo com arrays de diferentes tipos:

```json
{
  "frutas": ["maçã", "banana", "laranja"],
  "numeros": [1, 2, 3, 5, 8, 13],
  "booleanos": [true, false, true],
  "objetos": [
    { "id": 1, "nome": "item A" },
    { "id": 2, "nome": "item B" }
  ],
  "vazio": []
}
```

---

## 5. Servidor back-end e Web Service

### Servidor back-end

O back-end é o sistema responsável por processar requisições, gerenciar dados e fornecer respostas a clientes como navegadores, aplicações web e aplicativos móveis.

Suas principais responsabilidades são:

- Armazenar e recuperar dados;
- Executar regras de negócio;
- Validar informações recebidas;
- Fornecer APIs para a comunicação com outros sistemas;
- Controlar autenticação, autorização e tratamento de erros.

### Web Service

Um Web Service é um serviço acessível pela web que permite a comunicação entre sistemas por meio de HTTP ou HTTPS. Ele possibilita que aplicações desenvolvidas com linguagens, plataformas e tecnologias diferentes troquem dados de maneira padronizada.

Uma API REST criada com Express pode funcionar como um Web Service, pois disponibiliza recursos por endpoints HTTP.

---

## 6. Express.js

O **Express.js** é um framework minimalista, flexível e popular para Node.js. Ele simplifica a criação de servidores web e APIs REST.

### Principais recursos

- **Roteamento:** definição de caminhos como `/users` e `/products`;
- **Middlewares:** funções executadas durante o processamento de uma requisição, úteis para autenticação, logs, CORS e tratamento de erros;
- **Integração:** conexão facilitada com bancos de dados e outros serviços;
- **Produtividade:** menos código de infraestrutura em comparação com o módulo `http` puro do Node.js;
- **Desempenho:** adequado para APIs e servidores leves.

### Node.js puro e Express.js

Com o módulo `http` do Node.js, as rotas precisam ser verificadas manualmente:

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

Com Express, a rota fica mais clara e direta:

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Olá, mundo!');
});

app.listen(3000);
```

### Quando utilizar Express.js

O Express é indicado para:

- APIs REST;
- Integração com bancos de dados;
- Back-ends para aplicações web e mobile;
- Aplicações escaláveis;
- Servidores com templates;
- Autenticação, logs e tratamento de erros por meio de middlewares;
- Prototipagem rápida.

Para aplicações em tempo real, WebSockets costumam ser mais adequados. Para processamento pesado, a recomendação é utilizar Workers ou uma arquitetura específica para processamento assíncrono.

---

## 7. Criando uma API REST básica

### 7.1 Inicialização do projeto

Crie uma pasta para o projeto, abra-a no VS Code e inicialize o projeto Node.js:

```bash
npm init -y
npm install express cors
```

O pacote `express` fornece o framework da API. O pacote `cors` permite configurar o compartilhamento de recursos entre origens diferentes.

### 7.2 Arquivo `api.js`

```javascript
import express from 'express';
import cors from 'cors';

const app = express();

app.use(cors());
app.use(express.json());

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

Para executar:

```bash
node api.js
```

A API poderá ser acessada localmente em `http://localhost:3000`.

> Para utilizar a sintaxe `import`, configure o projeto com `"type": "module"` no `package.json`. Outra opção é usar a sintaxe CommonJS com `require`.

### CORS

**CORS** (*Cross-Origin Resource Sharing*) é um mecanismo de segurança do navegador que controla requisições entre origens diferentes. Ele é necessário quando, por exemplo, o front-end está em um domínio e a API está em outro.

O middleware `cors()` libera o acesso padrão durante o desenvolvimento:

```javascript
app.use(cors());
```

Em produção, é recomendável restringir as origens autorizadas em vez de liberar qualquer domínio.

---

## 8. Hospedagem com Render

O **Render** é uma plataforma de hospedagem em nuvem com suporte a Node.js, Python e outras tecnologias. A plataforma integra-se a repositórios Git e permite publicar APIs e microsserviços.

### Benefícios

- Deploy em poucos passos;
- Integração com GitHub;
- Deploy contínuo após novas alterações;
- Certificado SSL gratuito;
- Monitoramento de desempenho;
- Escalabilidade para aplicações profissionais;
- Interface adequada para projetos acadêmicos e protótipos.

### Publicando uma API

1. Faça o commit de todos os arquivos do projeto;
2. Envie o projeto para um repositório no GitHub;
3. Acesse o [dashboard do Render](https://dashboard.render.com/);
4. Crie um novo **Web Service**;
5. Conecte o repositório do GitHub;
6. Configure o comando de build e o comando de inicialização;
7. Execute o deploy;
8. Acesse a API pelo endereço fornecido, como `seu-projeto.onrender.com`.

Para o exemplo simples apresentado na aula:

- **Build Command:** `npm install`;
- **Start Command:** `node api.js`.

A porta deve ser obtida da variável de ambiente `PORT`, usando uma porta local como alternativa:

```javascript
const PORT = process.env.PORT || 3000;
```

---

## 9. Projeto de notas com CRUD

Na segunda parte da aula, a API é evoluída. Em vez de exibir apenas data e status, ela passa a armazenar, listar, editar e excluir notas.

CRUD é a sigla para as quatro operações fundamentais sobre dados:

| Operação | Significado | Método HTTP |
|---|---|---|
| **Create** | Criar | `POST` |
| **Read** | Consultar | `GET` |
| **Update** | Atualizar | `PUT` ou `PATCH` |
| **Delete** | Excluir | `DELETE` |

A aplicação utiliza:

- `server.js` para configurar e executar o servidor;
- `data.json` para armazenar as notas;
- Express.js para criar as rotas;
- Body Parser ou `express.json()` para ler o corpo das requisições;
- React para construir o front-end consumidor da API.

Projeto demonstrativo: [Notas App React](https://notas-app-react.vercel.app/).

### Rotas da aplicação

| Rota | Operação | Descrição |
|---|---|---|
| `GET /api/notes` | Listar | Retorna todas as notas. |
| `POST /api/notes` | Criar | Adiciona uma nota com `titulo` e `texto`. |
| `GET /api/notes/:id` | Consultar uma | Retorna uma nota específica pelo ID. |
| `PUT /api/notes/:id` | Atualizar | Atualiza o título e o texto de uma nota. |
| `DELETE /api/notes/:id` | Excluir | Remove uma nota pelo ID. |

Cada nota recebe um ID único, gerado com `Date.now().toString()`, e uma data de criação.

---

## 10. Implementação do CRUD

### 10.1 Instalação

Crie a pasta `projeto-notas`, abra-a no VS Code e instale as dependências:

```bash
npm init -y
npm install express cors
```

A aula apresenta o pacote `body-parser` para ler JSON enviado no corpo das requisições:

```bash
npm install body-parser
```

Em versões atuais do Express, `express.json()` já oferece esse recurso, evitando uma dependência adicional.

### 10.2 Arquivo `server.js`

```javascript
const express = require('express');
const fs = require('fs');
const cors = require('cors');

const app = express();
const PORT = process.env.PORT || 3000;
const FILE = 'data.json';

app.use(cors());
app.use(express.json());

function readNotes() {
  try {
    const data = fs.readFileSync(FILE, 'utf8');
    return JSON.parse(data);
  } catch {
    return [];
  }
}

function saveNotes(notes) {
  fs.writeFileSync(FILE, JSON.stringify(notes, null, 2));
}

app.get('/api/notes', (req, res) => {
  res.json(readNotes());
});

app.get('/api/notes/:id', (req, res) => {
  const notes = readNotes();
  const note = notes.find((item) => item.id === req.params.id);

  if (!note) {
    return res.status(404).json({ erro: 'Nota não encontrada' });
  }

  res.json(note);
});

app.post('/api/notes', (req, res) => {
  const { titulo, texto } = req.body;

  if (!titulo || !texto) {
    return res.status(400).json({ erro: 'titulo e texto são obrigatórios' });
  }

  const notes = readNotes();
  const newNote = {
    id: Date.now().toString(),
    titulo,
    texto,
    criadoEm: new Date().toISOString()
  };

  notes.push(newNote);
  saveNotes(notes);
  res.status(201).json(newNote);
});

app.put('/api/notes/:id', (req, res) => {
  const notes = readNotes();
  const noteIndex = notes.findIndex((item) => item.id === req.params.id);

  if (noteIndex === -1) {
    return res.status(404).json({ erro: 'Nota não encontrada' });
  }

  const { titulo, texto } = req.body;

  if (!titulo || !texto) {
    return res.status(400).json({ erro: 'titulo e texto são obrigatórios' });
  }

  notes[noteIndex].titulo = titulo;
  notes[noteIndex].texto = texto;
  saveNotes(notes);
  res.json(notes[noteIndex]);
});

app.delete('/api/notes/:id', (req, res) => {
  const notes = readNotes();
  const filteredNotes = notes.filter((item) => item.id !== req.params.id);

  if (filteredNotes.length === notes.length) {
    return res.status(404).json({ erro: 'Nota não encontrada' });
  }

  saveNotes(filteredNotes);
  res.status(204).send();
});

app.listen(PORT, () => {
  console.log(`Servidor rodando em http://localhost:${PORT}`);
});
```

### 10.3 Arquivo `data.json`

Crie o arquivo na raiz do projeto. Ele deve conter um array de notas:

```json
[
  {
    "id": "1",
    "titulo": "Lembretes",
    "texto": "Comprar leite e pão",
    "criadoEm": "2026-04-28T10:00:00Z"
  },
  {
    "id": "2",
    "titulo": "Tarefas do trabalho",
    "texto": "Enviar relatório até sexta-feira",
    "criadoEm": "2026-04-28T10:00:00Z"
  }
]
```

### 10.4 Leitura e gravação dos dados

- `fs.readFileSync()` lê o conteúdo do arquivo;
- `JSON.parse()` converte o texto JSON em um array JavaScript;
- `JSON.stringify()` converte o array em texto JSON;
- `fs.writeFileSync()` salva as alterações no arquivo;
- O bloco `try...catch` permite iniciar com um array vazio caso o arquivo ainda não exista ou esteja inválido.

Esse armazenamento é adequado para fins didáticos e pequenos testes. Em aplicações reais, um banco de dados é mais apropriado para concorrência, segurança, desempenho e integridade dos dados.

---

## 11. Fluxo completo da aplicação

O funcionamento esperado do projeto é:

1. O usuário interage com a interface React;
2. O React envia uma requisição HTTP para a API;
3. O Express identifica a rota e o método utilizado;
4. O servidor valida os dados recebidos;
5. O arquivo `data.json` é lido ou atualizado;
6. A API retorna uma resposta JSON e um status HTTP;
7. O React atualiza a interface com o resultado.

### Exemplos de requisição

Criar uma nota:

```http
POST /api/notes
Content-Type: application/json

{
  "titulo": "Estudar APIs",
  "texto": "Revisar métodos HTTP e CRUD"
}
```

Listar notas:

```http
GET /api/notes
```

Atualizar uma nota:

```http
PUT /api/notes/1
Content-Type: application/json

{
  "titulo": "Estudar APIs REST",
  "texto": "Praticar Express e integração com React"
}
```

Excluir uma nota:

```http
DELETE /api/notes/1
```

---

## 12. Status HTTP utilizados

| Status | Uso no projeto |
|---|---|
| `200 OK` | Consulta ou atualização concluída com sucesso. |
| `201 Created` | Nota criada com sucesso. |
| `204 No Content` | Nota excluída com sucesso, sem corpo na resposta. |
| `400 Bad Request` | Dados obrigatórios ausentes ou inválidos. |
| `404 Not Found` | Nota ou rota não encontrada. |

O uso adequado dos status ajuda o front-end a interpretar corretamente o resultado de cada requisição.

---

## 13. Publicação do projeto

### Back-end no Render

1. Execute e teste o servidor localmente com `node server.js`;
2. Envie o projeto Express para o GitHub;
3. Crie um **Web Service** no Render;
4. Configure o repositório conectado;
5. Use `npm install` como comando de build;
6. Use `node server.js` como comando de inicialização;
7. Copie a URL gerada pelo Render.

### Front-end na Vercel

1. Crie a interface React para listar, cadastrar, editar e excluir notas;
2. Configure o front-end para usar a URL online da API;
3. Substitua a URL local `http://localhost:3000/api/notes` pelo endpoint do Render;
4. Envie o projeto React para o GitHub;
5. Faça o deploy na Vercel;
6. Teste todas as operações CRUD em produção.

A separação entre front-end e back-end permite que cada aplicação seja publicada e atualizada de forma independente.

---

## 14. Atividades

### Atividade 01 — Atualização do repositório

1. Atualizar o repositório da disciplina com todos os arquivos e alterações realizadas;
2. Conferir se a versão publicada corresponde à versão final da atividade;
3. Verificar se todos os arquivos foram enviados corretamente;
4. Copiar o link do repositório atualizado;
5. Enviar o endereço pelo [formulário da atividade](https://forms.gle/L7iL7jx1RzyiXBnk9).

### Atividade 02 — API de notas

Evoluir o projeto Express para uma aplicação de notas com:

- Persistência em `data.json`;
- Listagem de notas;
- Criação de notas;
- Consulta por ID;
- Edição de notas;
- Exclusão de notas;
- Integração com um front-end React;
- Deploy do back-end no Render;
- Deploy do front-end na Vercel.

---

## 15. Síntese

Uma API REST organiza a comunicação entre aplicações por meio de recursos, endpoints, métodos HTTP e representações JSON. Com Node.js e Express.js, é possível criar rapidamente um servidor que recebe requisições, aplica regras de negócio e devolve respostas padronizadas.

O projeto de notas reúne os conceitos centrais da aula: criação de rotas, uso de middlewares, leitura do corpo das requisições, persistência de dados, operações CRUD, integração entre React e Express e publicação de aplicações na nuvem.

O fluxo essencial é:

> **React → requisição HTTP → API Express → dados → resposta JSON → atualização da interface**

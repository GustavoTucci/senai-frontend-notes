# Resumo da Aula 09 — Projeto React 02

## Objetivo da aula

A aula apresenta recursos essenciais para transformar uma interface React em uma aplicação interativa e com múltiplas páginas. Os principais temas são:

- gerenciamento de estado com `useState`;
- construção e validação de formulários;
- sincronização com recursos externos usando `useEffect`;
- consumo e envio de dados por APIs;
- navegação entre páginas com React Router.

## State e `useState`

**State** é uma informação mantida pelo componente que pode mudar durante o uso da aplicação, como o valor de um contador, o texto de um campo ou uma lista recebida de uma API. Quando o estado é alterado, o React renderiza novamente o componente e atualiza a interface.

Uma variável comum não é suficiente para controlar a tela porque:

- sua alteração não solicita uma nova renderização;
- seu valor pode ser recriado quando o componente é executado novamente;
- ela não oferece uma função própria para atualizar a interface.

O Hook `useState` recebe um valor inicial e retorna o valor atual junto com uma função de atualização:

```jsx
import { useState } from "react";

function Contador() {
  const [contador, setContador] = useState(0);

  return (
    <section>
      <p>Valor: {contador}</p>
      <button onClick={() => setContador(contador + 1)}>
        Incrementar
      </button>
    </section>
  );
}
```

Hooks são funções especiais do React. Seus nomes começam com `use`, e eles devem ser utilizados no início do componente ou de outro Hook, seguindo as regras do React.

## Formulários e campos controlados

Formulários permitem receber dados do usuário em situações como cadastro, login, busca e alteração de preferências. Em React, os valores dos campos podem ser controlados pelo estado:

```jsx
const [nome, setNome] = useState("");

<input
  value={nome}
  onChange={(evento) => setNome(evento.target.value)}
/>
```

Nesse fluxo:

1. o usuário digita no campo;
2. o evento `onChange` é disparado;
3. `evento.target.value` obtém o texto atual;
4. `setNome()` atualiza o estado;
5. o React renderiza o valor atualizado.

O envio do formulário é tratado com `onSubmit`. O método `preventDefault()` impede o comportamento padrão do navegador, evitando o recarregamento da página:

```jsx
function enviar(evento) {
  evento.preventDefault();
  alert("Formulário enviado!");
}

<form onSubmit={enviar}>
  <button type="submit">Enviar</button>
</form>
```

Durante o envio, a aplicação pode validar os dados, exibir mensagens de erro ou confirmar o sucesso da operação.

## `useEffect` e efeitos

Efeitos são ações realizadas fora da renderização da interface, normalmente para sincronizar o componente com sistemas externos. Alguns exemplos são:

- atualizar o título da aba;
- configurar temporizadores;
- registrar eventos do navegador;
- buscar dados de uma API.

O `useEffect` recebe uma função com o efeito e, opcionalmente, uma lista de dependências:

```jsx
useEffect(() => {
  document.title = titulo;
}, [titulo]);
```

Nesse exemplo, o efeito é executado novamente quando `titulo` muda. Quando o array de dependências é vazio (`[]`), o efeito é executado na montagem do componente.

### Limpeza de efeitos

Alguns efeitos criam recursos que precisam ser encerrados. Para isso, o `useEffect` pode retornar uma função de limpeza:

```jsx
useEffect(() => {
  window.addEventListener("resize", atualizar);

  return () => {
    window.removeEventListener("resize", atualizar);
  };
}, []);
```

A limpeza ocorre antes de uma nova configuração do efeito, quando suas dependências mudam, e quando o componente deixa de ser utilizado. Tudo o que for configurado e precisar ser encerrado deve ter uma limpeza correspondente.

## Consumo de APIs

Uma API (Application Programming Interface) permite a comunicação entre sistemas. Uma aplicação React pode consumir APIs para consultar produtos, usuários, publicações e outros dados, além de enviar informações para serviços externos.

O `fetch()` realiza requisições HTTP. Como a resposta é assíncrona, é necessário aguardar o resultado e converter o corpo para JSON:

```jsx
const resposta = await fetch(url);

if (!resposta.ok) {
  throw new Error("Erro na consulta");
}

const dados = await resposta.json();
```

Uma busca pode ser iniciada dentro de um `useEffect` e armazenada no estado:

```jsx
const [publicacoes, setPublicacoes] = useState([]);

useEffect(() => {
  async function carregar() {
    const resposta = await fetch(url);
    const dados = await resposta.json();
    setPublicacoes(dados);
  }

  carregar();
}, []);
```

Para enviar dados, utiliza-se normalmente o método `POST`, informando o formato do conteúdo e convertendo o objeto para JSON:

```jsx
await fetch("/api/publicacoes", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({ title: "Aprendendo React" }),
});
```

### Cuidados ao consumir APIs

- Tratar erros de rede com `try...catch`.
- Verificar `resposta.ok` e o status HTTP.
- Representar estados de carregamento, lista vazia e erro na interface.
- Evitar requisições repetidas causadas por dependências incorretas no `useEffect`.
- Não expor chaves secretas no código executado no navegador.
- Considerar autenticação, limites de uso e políticas de CORS.

## React Router

Aplicações React podem ter várias telas, como início, catálogo, detalhes e sobre. O roteamento associa caminhos da URL aos componentes exibidos e permite navegar entre páginas sem recarregar todo o documento.

O React Router utiliza os componentes `BrowserRouter`, `Routes` e `Route`:

```jsx
import {
  BrowserRouter,
  Routes,
  Route,
} from "react-router-dom";

<BrowserRouter>
  <Routes>
    <Route path="/" element={<Inicio />} />
    <Route path="/sobre" element={<Sobre />} />
  </Routes>
</BrowserRouter>
```

Conceitos importantes:

- **Rota:** regra que associa um caminho a uma interface.
- **URL:** endereço da página atual.
- **Link:** componente usado para navegar entre rotas.
- **Parâmetro:** parte variável do caminho.
- **Rota aninhada:** rota organizada dentro de uma estrutura pai.

Para navegar dentro da aplicação, usa-se `Link` e sua propriedade `to`:

```jsx
import { Link } from "react-router-dom";

<nav>
  <Link to="/">Início</Link>
  <Link to="/sobre">Sobre</Link>
</nav>
```

Parâmetros são úteis para páginas de detalhes. Em uma rota como `/conceitos/:id`, o Hook `useParams()` permite acessar o valor de `id`:

```jsx
const { id } = useParams();

return <h1>Conceito: {id}</h1>;
```

## Relação entre os conceitos

Uma aplicação React completa pode combinar os recursos da aula da seguinte forma:

1. `useState` armazena os dados e as informações de controle da interface.
2. Formulários recebem e validam dados por meio de campos controlados.
3. `useEffect` inicia a comunicação com APIs quando necessário.
4. Os dados obtidos são armazenados no estado e renderizados na tela.
5. O React Router organiza diferentes telas e permite acessar detalhes por parâmetros de URL.

## Atividade proposta

Desenvolver uma aplicação React que utilize todos os conceitos estudados:

- State e `useState`;
- formulários;
- `useEffect`;
- consumo de APIs;
- React Router.

Também é necessário criar um repositório público no GitHub e um `README` com a descrição do projeto, suas funcionalidades e os conceitos utilizados.

## Materiais complementares

- [Conceitos de React](https://github.com/deivisontakatu/aula-react)
- [Exemplo de projeto React](https://github.com/deivisontakatu/projeto-react)
- [Aplicação de exemplo](https://projeto-react-five-swart.vercel.app/)

# Resumo da Aula 08 — Projeto React

## Objetivo da aula

A aula revisa conceitos importantes de JavaScript e apresenta fundamentos para organizar interfaces com React. O foco está em descrever a interface com JSX, dividi-la em componentes reutilizáveis, enviar dados entre componentes e renderizar listas e conteúdos condicionais.

## Revisão de JavaScript

Antes de introduzir React, o material retoma:

- **Variáveis e tipos:** uso de `const` e `let`, diferença entre maiúsculas e minúsculas nos nomes e tipos como `String`, `Number`, `Boolean`, `undefined`, `null`, objetos e arrays.
- **Operadores:** operações aritméticas, comparações (incluindo `===`), operadores lógicos e atribuições compostas.
- **Condicionais e repetições:** `if`, `else if`, `else`, operador ternário, `for`, `while`, `do...while`, `break` e `continue`.
- **Funções:** funções tradicionais e arrow functions, parâmetros e retorno com `return`.
- **Arrays e objetos:** acesso por índice, `length`, `forEach()` e `filter()`; propriedades e métodos de objetos, com `this` para referenciar o próprio objeto.
- **DOM:** seleção de elementos com `getElementById()` e `querySelector()`, eventos com `addEventListener()` e alterações de conteúdo, valores e classes.

## JSX

JSX é uma extensão de sintaxe que permite descrever estruturas semelhantes a HTML dentro do JavaScript. É usado para expressar a interface dos componentes React e aceita expressões JavaScript entre chaves, como `{nome}` ou `{a + b}`. O JSX é transformado em JavaScript antes da execução.

Convenções destacadas na aula:

- Use `className` em vez de `class` e `htmlFor` em vez de `for`.
- Feche elementos sem conteúdo, como `<img />`.
- Um componente deve retornar um elemento raiz ou usar um Fragment.
- Insira valores e expressões JavaScript entre `{}`.

## Componentes

Componentes são partes independentes e reutilizáveis da interface, normalmente definidas como funções JavaScript que retornam elementos React. Seus nomes começam com letra maiúscula e eles são utilizados em JSX com a sintaxe `<NomeDoComponente />`.

Uma página pode ser composta por componentes menores — por exemplo, cabeçalho, busca, lista de produtos, cartões e rodapé. Essa composição forma uma árvore: um componente principal contém componentes filhos, que podem conter outros componentes. A divisão facilita a organização e permite reutilizar estruturas sem repetir código.

## Props e fluxo de dados

**Props** (properties) são dados recebidos por um componente. Em uma estrutura comum, o componente pai fornece esses dados ao filho, que os utiliza para apresentar conteúdo. Assim, o mesmo componente pode manter sua estrutura e exibir informações diferentes em cada uso.

As props podem conter strings, números, valores booleanos, arrays, objetos, funções ou elementos React. Por exemplo, um componente `CardConceito` pode receber `titulo` e `descricao`; um componente `Saudacao` pode receber `nome`.

## DOM, Virtual DOM e atualização da interface

O **DOM** representa a estrutura do documento HTML no navegador e pode ser consultado ou modificado por JavaScript. Alterar manualmente cada elemento pode tornar interfaces complexas difíceis de manter.

A aula apresenta o **Virtual DOM** como uma representação da interface em memória usada pelo React para coordenar atualizações. Em termos gerais, quando os dados mudam, os componentes relevantes são executados novamente, o React compara a nova descrição da interface com a anterior (reconciliação) e aplica as mudanças necessárias ao ambiente de renderização, como o DOM do navegador. Portanto, o desenvolvedor descreve o resultado esperado em vez de atualizar manualmente cada elemento.

A identidade dos elementos ajuda o React a relacionar partes da interface entre renderizações. Em listas, as `key` ajudam a identificar itens; chaves estáveis permitem associar os mesmos itens quando a coleção muda.

## Listas e keys

Para transformar dados de um array em elementos de interface, usa-se normalmente `map()`, que gera um elemento para cada item. Cada elemento renderizado em uma lista deve ter uma `key` que o identifique entre seus elementos irmãos — geralmente um identificador associado ao próprio dado, como `id`.

`filter()` pode selecionar os itens que atendem a uma condição, e o resultado pode ser renderizado com `map()`. Ao atualizar listas mantidas em estado, o material recomenda produzir novos arrays em vez de modificar diretamente o array existente.

## Renderização condicional

A renderização condicional permite adaptar o conteúdo exibido a props, estado ou dados:

- Use `if` e `return` quando cada condição exigir uma interface diferente.
- Use o operador ternário (`condição ? valorSeVerdadeiro : valorSeFalso`) para alternar entre alternativas simples, como uma mensagem de carregamento e o resultado.
- Considere situações como listas vazias, carregamento, erro e sucesso, refletindo o estado real dos dados.

## Atividade proposta

Desenvolver uma aplicação React que utilize os conceitos da aula: JSX, componentes, props, Virtual DOM, listas e renderização condicional. A atividade também solicita criar um repositório público no GitHub e um `README` com a descrição, as funcionalidades e os conceitos utilizados.

## Materiais complementares indicados

- [Conceitos de React](https://github.com/deivisontakatu/aula-react)
- [Exemplo de projeto React](https://github.com/deivisontakatu/projeto-react)
- [Aplicação de exemplo](https://projeto-react-five-swart.vercel.app/)
- [Documentação do React](https://react.dev)
- [Revisão de JavaScript](https://github.com/deivisontakatu/aula-javascript)

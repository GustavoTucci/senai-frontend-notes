# 🚀 Resumo — Aula 03: Projetos com Frameworks Front-end

## 1. O que são Frameworks Front-end?

Um **framework front-end** é um conjunto de ferramentas, bibliotecas e convenções que padroniza o desenvolvimento de interfaces web.

Ele fornece uma estrutura pré-definida para acelerar a criação de aplicações complexas.

### Desenvolvimento sem framework

- Código desenvolvido manualmente;
- Maior repetição;
- Manutenção mais difícil;
- Menor padronização.

### Desenvolvimento com framework

- Componentes reutilizáveis;
- Gerenciamento de estado;
- Atualizações eficientes da interface;
- Maior organização e escalabilidade.

---

## 2. Framework × Biblioteca

### Framework

O framework **controla o fluxo da aplicação**, utilizando o conceito de **inversão de controle**.

Características:

- Possui estrutura definida;
- Impõe determinados padrões;
- Controla quando determinadas partes da aplicação são executadas.

**Exemplos:** Angular e Vue.

### Biblioteca

Na biblioteca, **o desenvolvedor controla quando e como utilizar seus recursos**.

Características:

- Mais flexível;
- Menos imposições;
- O desenvolvedor decide quando chamar suas funcionalidades.

**Exemplos:** React e jQuery.

> **Resumo:** biblioteca → você chama.  
> framework → ele controla o fluxo.

---

## 3. Por que utilizar Frameworks?

Os frameworks oferecem diversas vantagens:

- ⚡ **Maior produtividade** — soluções prontas para roteamento, estado e renderização;
- 🧩 **Melhores práticas** — organização baseada em componentes;
- 🔧 **Manutenção facilitada** — otimizações internas como Virtual DOM e Change Detection;
- 🌎 **Comunidade e suporte** — documentação, plugins e soluções disponíveis.

---

## 4. Principais tecnologias estudadas

| Tecnologia | Característica principal |
|---|---|
| **React** | Biblioteca JavaScript para interfaces |
| **Angular** | Framework completo |
| **Vue.js** | Framework progressivo |
| **Next.js** | Framework baseado em React |

A escolha da tecnologia deve considerar fatores como **complexidade do projeto, curva de aprendizado, desempenho, escalabilidade e comunidade**.

---

# ⚛️ 5. React

O **React**, criado pelo Facebook em 2013, é apresentado na aula como uma **biblioteca JavaScript**, e não como um framework.

É utilizado para criar:

- Web Apps;
- Interfaces dinâmicas;
- Componentes reutilizáveis;
- Aplicações escaláveis.

Sua arquitetura utiliza **componentes** e **Virtual DOM**.

## Conceitos importantes

### Hooks

**useState**

Utilizado para gerenciar o estado de um componente funcional.

**useEffect**

Utilizado para lidar com efeitos colaterais, como chamadas de API.

### JSX

Permite escrever uma estrutura semelhante ao HTML dentro do JavaScript.

Principais diferenças:

```jsx
className
```

em vez de:

```html
class
```

Expressões JavaScript são utilizadas entre:

```jsx
{ }
```

As tags devem ser fechadas:

```jsx
<img />
```

### Gerenciamento de estado

- **Context API** → indicada para estados menores;
- **Redux** → indicada para estados mais complexos e compartilhados globalmente.

---

# 🌳 6. DOM e Virtual DOM

O **DOM (Document Object Model)** representa a estrutura de uma página HTML em forma de árvore.

O JavaScript pode utilizar o DOM para alterar o conteúdo da página.

O **Virtual DOM**, utilizado pelo React, funciona como uma representação do DOM.

Quando ocorre uma alteração:

1. O React atualiza o Virtual DOM;
2. Compara a nova versão com a anterior;
3. Identifica o que mudou;
4. Aplica somente as alterações necessárias no DOM real.

Isso permite atualizações mais eficientes da interface.

---

# 🅰️ 7. Angular

O **Angular**, desenvolvido pelo Google, é apresentado como um **framework completo**.

Entre seus recursos estão:

- Roteamento;
- HTTP Client;
- Injeção de dependências;
- TypeScript;
- Arquitetura MVC;
- Angular CLI;
- Change Detection.

## Conceitos fundamentais

### Componentes

Utilizam:

```text
@Component
```

e podem reunir:

- HTML;
- CSS;
- TypeScript.

### Módulos

Utilizam:

```text
@NgModule
```

para organizar a aplicação em blocos funcionais.

### Serviços

Utilizam:

```text
@Injectable
```

para criar lógica reutilizável.

### Data Binding

Exemplos apresentados:

```text
[(ngModel)]
```

Two-way binding.

```text
{{ }}
```

Interpolação.

### Outros conceitos

- Injeção de dependência;
- Roteamento;
- RouterModule.

---

# 🛠️ 8. Criando um projeto Angular

### 1. Instalar o Angular CLI

```bash
npm install -g @angular/cli
```

### 2. Criar o projeto

```bash
ng new meu-app-angular
```

### 3. Entrar na pasta

```bash
cd meu-app-angular
```

### 4. Abrir no VS Code

```bash
code .
```

### 5. Executar

```bash
ng serve
```

O **Angular CLI** é uma ferramenta de linha de comando utilizada para criar, gerenciar e construir projetos Angular.

---

# 📁 9. Estrutura de um projeto Angular

Principais elementos:

```text
node_modules/
public/
src/
.angular/
.vscode/
.gitignore
package.json
package-lock.json
.editorconfig
README.md
angular.json
tsconfig.json
```

### `node_modules`

Armazena os pacotes e dependências instalados.

### `public`

Armazena arquivos estáticos públicos.

### `src`

Principal diretório do código-fonte.

### `.gitignore`

Define arquivos e diretórios que não devem ser versionados pelo Git.

### `package.json`

Gerencia dependências e scripts.

### `angular.json`

Configura aspectos como:

- Build;
- Testes;
- Estilos globais.

### `tsconfig.json`

Define configurações do TypeScript.

---

# 🟢 10. Vue.js

O **Vue.js** é apresentado como um framework progressivo.

Características:

- Fácil adoção gradual;
- Programação reativa;
- Arquitetura baseada em componentes;
- Single-File Components;
- Curva de aprendizado suave;
- Boa performance.

## Single-File Components

Os componentes Vue utilizam arquivos:

```text
.vue
```

que podem reunir:

- HTML;
- CSS;
- JavaScript.

---

# 🛠️ 11. Criando um projeto Vue

### Criar projeto

```bash
npm create vue@latest
```

### Entrar na pasta

```bash
cd meu-projeto-vue
```

### Instalar dependências

```bash
npm install
```

### Abrir no VS Code

```bash
code .
```

### Executar

```bash
npm run dev
```

---

# 📁 12. Estrutura de um projeto Vue

Principais elementos:

```text
node_modules/
public/
src/
assets/
components/
App.vue
main.js
index.html
vite.config.js
```

### `assets`

Arquivos como:

- Imagens;
- Fontes;
- CSS global.

### `components`

Armazena componentes reutilizáveis.

Exemplo:

```text
Button.vue
Header.vue
```

### `App.vue`

Componente raiz da aplicação.

### `main.js`

Ponto de entrada do Vue.

### `index.html`

HTML principal da SPA, contendo o elemento onde o Vue será montado.

### `vite.config.js`

Configurações do Vite, como:

- Build;
- Plugins;
- Proxies.

---

# ▲ 13. Next.js

O **Next.js** é um framework baseado em React para desenvolvimento de aplicações web modernas e full-stack.

Ele adiciona recursos ao React, como:

- Roteamento baseado em arquivos;
- Renderização no servidor;
- Server Components;
- Otimização de imagens;
- Otimização de fontes;
- Páginas e layouts;
- APIs;
- Recursos de backend;
- Otimizações de desempenho;
- SEO.

---

# 🛠️ 14. Criando um projeto Next.js

### Criar projeto

```bash
npx create-next-app@latest meu-projeto
```

### Entrar na pasta

```bash
cd meu-projeto
```

### Abrir no VS Code

```bash
code .
```

### Executar

```bash
npm run dev
```

---

# 📂 15. Estrutura do Next.js

Com o **App Router**, a pasta principal é:

```text
app/
```

Ela contém:

- Páginas;
- Layouts;
- Estilos globais;
- Componentes relacionados à aplicação.

Um conceito importante é:

```text
page.js
```

As pastas determinam a organização das rotas da aplicação.

---

# 🔄 16. Importando projetos prontos

Uma prática apresentada na aula é utilizar projetos existentes como base para acelerar o desenvolvimento.

A comunidade **open source** disponibiliza projetos gratuitos que podem ser:

- Clonados;
- Estudados;
- Personalizados;
- Utilizados como referência.

### Plataformas citadas

- **GitHub** — pesquisa de repositórios;
- **Vercel** — templates;
- **CodeSandbox** — templates e projetos.

No GitHub, é possível utilizar:

```bash
git clone <url>
```

para clonar um projeto.

---

# 🔀 17. Git e Versionamento

O desenvolvimento dos projetos deve utilizar **Git** para controle de versão.

O Git permite manter um histórico das alterações realizadas durante o desenvolvimento.

Na atividade proposta, cada projeto deverá ser publicado no **GitHub**, mantendo um histórico de commits que registre sua evolução.

---

# 📝 18. Atividade da aula

A atividade consiste em desenvolver, **em grupo**, quatro projetos Web sobre o mesmo tema:

1. ⚛️ **React**
2. 🟢 **Vue**
3. 🅰️ **Angular**
4. ▲ **Next.js**

Cada projeto deve possuir:

- Página funcional;
- Design responsivo;
- Organização;
- Componentes;
- Utilização dos recursos básicos da tecnologia escolhida.

Além disso, deve ser desenvolvido:

5. **Uma cópia de um projeto obtido a partir de um repositório.**

---

# 🧠 Resumo para prova

> **Framework Front-end** → estrutura e ferramentas para facilitar o desenvolvimento de interfaces.

> **Biblioteca** → você controla quando utiliza seus recursos.

> **Framework** → ele controla o fluxo da aplicação.

> **React** → biblioteca JavaScript baseada em componentes e Virtual DOM.

> **Angular** → framework completo, utiliza TypeScript e possui Angular CLI.

> **Vue** → framework progressivo, baseado em componentes e reatividade.

> **Next.js** → framework baseado em React, com recursos para aplicações modernas e full-stack.

> **Virtual DOM** → representação utilizada pelo React para tornar atualizações da interface mais eficientes.

> **Componentização** → divisão da aplicação em componentes reutilizáveis.

> **Git** → controle de versão e histórico das alterações.

> **GitHub** → hospedagem dos repositórios e colaboração.

## ⭐ O que estudar com mais atenção

**Framework × Biblioteca → React → Angular → Vue → Next.js → Componentização → Virtual DOM → Estrutura de projetos → npm → Git/GitHub.**

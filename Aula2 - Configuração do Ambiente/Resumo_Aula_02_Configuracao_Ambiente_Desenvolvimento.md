# 📚 Aula 02 — Configuração do Ambiente de Desenvolvimento

## 🎯 Objetivo

Configurar o ambiente necessário para desenvolver aplicações Front-end, conhecendo **versionamento, Git, VS Code, Node.js, NPM, React e Vercel**.

---

## 🔄 Versionamento

**Versionamento** é o processo de identificar e registrar diferentes versões de um software ou documento.

Permite:

- Registrar o que foi alterado, por quem e quando;
- Acompanhar o histórico do projeto;
- Recuperar versões anteriores;
- Trabalhar em equipe com mais segurança;
- Evitar perda de trabalho.

### Versionamento × Backup

| Versionamento | Backup |
|---|---|
| Registra o histórico das alterações | Guarda uma cópia do estado atual |
| Mostra quem, quando e por que alterou | Não possui rastreabilidade detalhada |
| Permite colaboração | Normalmente trabalha com uma cópia |
| Permite reversão de alterações específicas | Restaura o estado salvo |

---

## 🏷️ Versionamento Semântico (SemVer)

Segue o padrão:

```text
MAJOR.MINOR.PATCH
```

- **MAJOR** → mudança incompatível com versões anteriores.
- **MINOR** → nova funcionalidade compatível.
- **PATCH** → correção de bugs sem alteração da API.

### Exemplos

```text
1.0.0 → primeira versão estável
1.1.0 → nova funcionalidade compatível
1.1.1 → correção de bug
2.0.0 → mudança incompatível
```

### Tipos de alterações

- **Bug Fix** → correção de erros;
- **New Feature** → nova funcionalidade;
- **Feature Enhancement** → melhoria de funcionalidade existente;
- **Refactoring** → reorganização do código;
- **Performance** → otimização;
- **Security Patch** → correção de vulnerabilidades;
- **Dependency Update** → atualização de dependências;
- **Adding Tests** → inclusão de testes.

---

## 🌿 Git

**Git** é um sistema de controle de versão utilizado para registrar alterações e gerenciar diferentes versões de um projeto.

Permite:

- Baixar e enviar código para repositórios online;
- Registrar alterações;
- Restaurar versões anteriores;
- Trabalhar com branches;
- Colaborar com outros desenvolvedores.

### Configuração inicial

```bash
git --version

git config --global user.name "<Nome>"
git config --global user.email "<Email>"
```

---

## 🏷️ Tags

**Tags** são marcadores utilizados para identificar pontos importantes do histórico, principalmente versões e releases.

Exemplo:

```bash
git tag
git tag 1.0.0
git push origin 1.0.0
```

Podem ser:

- **Lightweight** → apenas um nome associado ao commit;
- **Annotated** → contém informações adicionais, como autor, data e mensagem.

---

## ✅ Boas práticas com Git

- Fazer **commits pequenos e frequentes**;
- Criar mensagens de commit claras;
- Utilizar **branches** para novas funcionalidades e correções;
- Manter a branch principal estável;
- Testar o código antes de realizar o merge.

---

## 💻 IDE e Visual Studio Code

**IDE (Integrated Development Environment)** é um ambiente que reúne ferramentas para desenvolver, testar, executar e depurar software.

O **Visual Studio Code (VS Code)** é um editor de código que, por meio de extensões e ferramentas integradas, oferece recursos típicos de uma IDE.

---

## 🟢 Node.js

**Node.js** é um ambiente de execução JavaScript que permite executar código no **backend/servidor**.

Uma de suas vantagens é permitir o uso de **JavaScript tanto no navegador quanto no servidor**, aproximando Front-end e Back-end.

Verificar instalação:

```bash
node --version
```

---

## 📦 NPM

**NPM (Node Package Manager)** é o gerenciador de pacotes do Node.js.

É utilizado para:

- Instalar bibliotecas e frameworks;
- Atualizar e remover dependências;
- Gerenciar pacotes do projeto;
- Compartilhar módulos.

O arquivo **`package.json`** registra as dependências e informações do projeto.

Para instalar as dependências:

```bash
npm install
```

---

## ⚛️ Criando um Projeto React

O material apresenta a criação de um projeto React utilizando:

```bash
npx create-react-app meu-projeto-react
```

### Passos

```bash
npx create-react-app meu-projeto-react
cd meu-projeto-react
code .
npm start
```

O `npx` é um executor de pacotes do NPM.

O projeto criado possui uma estrutura inicial com ferramentas de build, Babel, servidor local e scripts de desenvolvimento.

### Principais arquivos e pastas

- **`node_modules/`** → pacotes e dependências instaladas;
- **`public/`** → arquivos públicos, como HTML, JSON e imagens;
- **`src/`** → arquivos React/JavaScript do projeto;
- **`.gitignore`** → define arquivos e diretórios ignorados pelo Git;
- **`package.json`** → informações e dependências do projeto;
- **`package-lock.json`** → informações de instalação das dependências;
- **`index.js`** → ponto de entrada do React;
- **`App.js`** → componente raiz;
- **`App.css`** → estilos do componente App;
- **`index.css`** → estilos globais.

---

## 🚀 Deploy

**Deploy** é o processo de colocar uma aplicação em produção para que ela fique disponível aos usuários.

Etapas comuns:

1. Compilação;
2. Configuração do ambiente;
3. Testes finais;
4. Publicação.

---

## ▲ Vercel

A **Vercel** é uma plataforma utilizada para deploy e hospedagem de aplicações web modernas.

Principais características:

- Integração com **GitHub, GitLab e Bitbucket**;
- Deploy automático após um `push`;
- Suporte a React, Next.js, Vue e outros frameworks;
- Deploys rápidos e possibilidade de rollback;
- Serverless Functions;
- CDN global;
- Foco em performance e escalabilidade.

### Fluxo apresentado na aula

```text
React
  ↓
Git
  ↓
GitHub
  ↓
Vercel
  ↓
Aplicação online
```

---

## 📝 Atividade Prática

Criar uma aplicação React utilizando o **VS Code**, depois:

1. Versionar o projeto com Git;
2. Fazer commit e push para um repositório no GitHub;
3. Conectar o repositório à Vercel;
4. Realizar o deploy;
5. Disponibilizar o projeto por meio de uma URL pública da Vercel.

### Atividade complementar

Em grupos, escolher um **Framework Front-end** e elaborar um **relatório técnico em PDF**, com no mínimo 5 páginas, apresentando:

- Principais características;
- Vantagens;
- Aplicações no mercado;
- Exemplo de utilização em um projeto Web.

---

## 🧠 Resumo rápido

> **Git** → controla versões do código.  
> **GitHub** → armazena o repositório online.  
> **VS Code** → ambiente/editor para desenvolvimento.  
> **Node.js** → executa JavaScript no servidor e fornece o ambiente para ferramentas do ecossistema.  
> **NPM** → gerencia pacotes e dependências.  
> **React** → utilizado para desenvolver a aplicação Front-end.  
> **Vercel** → realiza o deploy e disponibiliza a aplicação online.

### 🔗 Fluxo geral

**VS Code → React → Git → GitHub → Vercel → Aplicação online**

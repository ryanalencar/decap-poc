---
title: ReactJs
---
### O que é Reactjs

O React é uma biblioteca front-end JavaScript de código aberto com foco em criar interfaces de usuário em páginas web. A biblioteca [Reactjs](https://react.dev/) e a linguagem de programação [Typescript](https://www.typescriptlang.org/pt/docs/) são homologadas pelo Banco do Nordeste para desenvolvimento das aplicações Front-end.

### Ferramenta de desenvolvimento

É recomendado o uso do [Visual Studio Code](https://code.visualstudio.com/).

### Pré-Requisitos

Necessário que os projetos sejam criados nas seguintes versões:

- [Node v18](https://nodejs.org/en/download/)
- [Yarn 1.22.19](https://classic.yarnpkg.com/en/docs/install/#windows-stable)
- [Reactjs 18](https://react.dev/)

### Configuração de ambiente

Antes de criar uma aplicação Reactjs é necessário configurar a máquina e para isso é disponibilizado o [guia de configuração de ambiente](https://docs.dreads.bnb/arquitetura/reactjs/configuração-de-ambiente/).

### Como criar uma aplicação Reactjs com Typescript

Nós vamos utilizar o comando create-react-app. Esse comando é a maneira oficial para criar uma aplicação REACT, oferecendo uma construção moderna, sem configurações.

Como o uso do Typescript é obrigatório, iremos inicializar a instalação junto com o create-react-app.

```shell.vs
$ npx create-react-app my-app --template typescript
```

```shell.vs
$ cd my-app
```

```shell.vs
$ npm start
```

{{< notice warning >}}

Se você já instalou anteriormente create-react-app via global npm install -g create-react-app, recomendamos que você desinstale o pacote usando npm uninstall -g create-react-app para garantir que o npx sempre use a versão mais recente.

{{< /notice >}}

O npm start faz com que o browser default do computador seja chamado, mas se precisar abra *<https://localhost:3000/>*

Quando estiver pronto para implantar na produção, crie um pacote reduzido com npm run build, mas atenção:

Para publicar seu APP no servidor do banco, deve-se incluir a seguinte prioridade no package.json:

```tsx
"homepage": ".",
```

{{< notice warning >}}

Isso vai garantir que todos os assets estão com caminho relativo ao index.html.
Você não precisa instalar ou configurar ferramentas como Webpack ou Babel. Eles são pré-configurados e ocultos para que você possa se concentrar no código.
{{< /notice >}}

![screencast](uploads/screencast.svg)
Para maiores informações: <https://facebook.github.io/create-react-app/docs/getting-started>

### Não suporte do internet explorer

A utilização das aplicações REACT através do navegador “Internet Explorer”, em todas as suas versões, não receberá suporte da arquitetura. Visto que, há problemas de compatibilidade entre as tecnologias e sendo assim, não podemos garantir que as aplicações não estarão vulneráveis a ataques, eventuais falhas ou bugs no futuro.

Para isso, vamos colocar o alerta na página html da nossa aplicação:

Na sua aplição > pasta PUBLIC > index.html

```tsx
<script>
    var agent= String(navigator.userAgent);
    var isIE7 = agent.match(/MSIE/gi);
    var isIE11 = agent.match(/clr/gi);

    if(isIE11||isIE7){
        alert("Navegador não suportado! É recomendada a utilização dos seguintes navegadores: Google Chrome, Mozilla Firefox ou Microsoft Edge.");
    }
</script>
```

### A biblioteca de componentes BNB-UI

O BNB-UI é uma biblioteca de componentes do Banco do Nordeste, que tem o propósito de fornecer as diretrizes comuns que devem ser seguidas por todos os que realizam atividades de desenvolvimento, manutenção e evolução nas aplicações web do Banco do Nordeste, de forma a assegurar uma identidade visual única de acordo com as normas da organização, padrões de qualidade e políticas organizacionais.

Para mais informações acesse [aqui](https://docs.dreads.bnb/ui-ux/bnb-ui/).

### Base de conhecimento de Erros

Página voltada para a documentação de erros conhecidos do time em ReactJS. Página ainda em construção, mas que já existe uma compilação detalhada de alguns erros, problemas comuns e soluções que nossa equipe encontrou ao desenvolver em React. 

Para mais informações acesse [aqui](../reactjs/base-de-conhecimento-de-erros/).

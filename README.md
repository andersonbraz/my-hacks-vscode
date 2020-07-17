# Hacks VSCode

## ESLint + Prettier 

[Fonte: ROBERTO ACHAR](https://robertoachar.dev/blog/eslint-prettier){:target="_blank"}

Como resolver o conflito entre o ESLint e o Prettier

---

## O que é lint?

Lint é o termo utilizado para análise estática de código e seu objetivo é encontrar problemas no código antes mesmo dele ser executado. É uma das etapas mais importantes da construção de um software.

## O que é ESLint?

ESLint é uma ferramenta de linting desenvolvida especificamente para JavaScript. Possui uma grande quantidade de regras pré-definidas e é completamente customizável através de plugins.

Para mais informações, acesse o site oficial do ESLint.

## O que é Prettier?

Prettier é um formatador de códigos com suporte a muitas linguagens e possui integração com a maioria dos editores de código. Seu objetivo é fazer com que o código seja formatado de maneira sólida e consistente.

O Prettier pode ser integrado ao ESLint para sobrescrever as regras definidas pelo ESLint.

Para mais informações, acesse o site oficial do Prettier.

## Conflito

Tanto o ESLint quanto o Prettier possuem extensões para o VS Code. Quando as duas extensões estão habilitadas no VS Code, as duas extensões vão tentar formatar o código e isso irá gerar conflito.

Para resolver esse problema, é necessário alterar as configurações do VS Code para que apenas uma das extensões formate o código.

## Solução

01. Instalar as dependências do ESLint

```shell
$ npm i -D eslint
```

02. Instalar as dependências do Prettier

```shell
$ npm i -D prettier eslint-config-prettier eslint-plugin-prettier
```

03. Criar o arquivo de configuração do ESLint (.eslintrc.json) e adicionar as regras do Prettier

```javascript
{
  "extends": ["prettier"],
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": [
      "error",
      {
        "singleQuote": true
      }
    ]
  }
}
````

04. Configurar o VS Code para que apenas a extensão do ESLint formate o código.

```javascript
{
  // habilitar o format on save (formatar ao salvar)
  "editor.formatOnSave": true,
  // configurar as ações que devem ser executadas ao salvar um arquivo
  "editor.codeActionsOnSave": {
    // executar o ESLint
    "source.fixAll.eslint": true
  },
  // desabilitar o plugin do Prettier para arquivos .js e .jsx
  "prettier.disableLanguages": ["javascript", "javascriptreact"]
}
```

## Conclusão

Essa é a maneira que encontrei para que as duas extensões possam conviver juntas e não haja conflito na hora de salvar/formatar os arquivos. Eu adiciono as configurações do Prettier dentro do arquivo de configurações do ESLint e desabilito a extensão do Prettier para arquivos dos tipos .js e .jsx.

---

## My Hacks

[Anderson Braz](https://www.andersonbraz.com);

## Arquivo do Workspace (.vscode\settings.json)

```javascript
{
  // habilitar o format on save (formatar ao salvar)
  "editor.formatOnSave": true,
  // configurar as ações que devem ser executadas ao salvar um arquivo
  "editor.codeActionsOnSave": {
    // executar o ESLint
    "source.fixAll.eslint": true
  },
  // desabilitar o plugin do Prettier para arquivos .js e .jsx
  "prettier.disableLanguages": ["javascript", "javascriptreact"],
  //
  "eslint.options": {
    "useEslintrc": false,
    "parserOptions": {
      "ecmaVersion": 2017
    },
    "env": {
      "es6": true
    }
  },
  "javascript.suggestionActions.enabled": false
}
```

## Arquivo do Workspace (.eslintrc.json)

```javascript
{
  "extends": ["prettier"],
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": [
      "error",
      {
        "singleQuote": true
      }
    ]
  }
}
```

## Arquivo do Workspace (.jshintrc)

```javascript
{
    "esversion": 6
}
```

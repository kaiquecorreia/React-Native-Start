# React Native Start
  Estrutura inicial de um projeto React Native, já com ambiente de desenvolvimento configurado.
  
## Pré-requisitos  

  1 - *[React Native Docs](https://facebook.github.io/react-native/docs/getting-started) Leia atentamente a documetação;*
  
  2 - Configurar o ambiente para rodar o react native, pode consultar diretamente na documentação;
  
  3 - Instalar o *React Native CLI - IMPORTANTE;*
  
  4 - Este projeto inicial utiliza o yarn para gerenciador de pacotes;


## Criando o projeto

  1 - Abrir um terminal e acessar pasta do projeto:
  ```
  cd pasta-do-projeto
  ```
  2 - Executar o comando do cli do React Native: 
  ```
  react-native init nome-do-projeto
  ```
  
### Testar App inicial:
  
  1 - Acessar pasta do projeto criado
  
  ```
  cd nome-do-projeto
  ```
  2 - Executar comando de acordo com a plataforma desejada:
  
  ```
  react-native run-ios
  ```
  
  ou
  
  ```
  react-native run-android
  ```
  
## Estruturando pastas do projeto

   1 - Criar pasta src dentro da raiz do projeto;
   
   2 - Colocar arquivo App.js dentro da pasta src;
   
   3 - Renomear para index.js;
   
   4 - Alterar o arquivo index.js na raiz do projeto da seguinte maneira: 
   
   ```
   import { AppRegistry } from 'react-native';
   import App from './src';
   import { name as appName } from './app.json';

   AppRegistry.registerComponent(appName, () => App);
   
   ```
## Configurando Dependências

   Instalando dependências iniciais importantes para o projeto.

### PropTypes - Validação de propriedades
  
   1 - Abra um terminal e digite o seguinte comando:
   
   ```
   yarn add prop-types
   ```
   
   2 - Exemplo de utilização
   
   A) StateFul component
    
          
          import React, { Component } from 'react';
          import { View, Text } from 'react-native';
          import PropTypes from 'prop-types';

          export default class Greeting extends Component {
            const { name } = this.props;
              render() {
                return (
                  <View>
                    <Text>Hello, {name}</Text>
                  </View>

                );
              }

              static propTypes = {
                name: PropTypes.string
              }
          }

          
    
   B) StateLess component
    
         
          import Reactfrom 'react';
           import { View, Text } from 'react-native';
          import PropTypes from 'prop-types';

          const Greeting = ({name}) => (
                <View>
                  <Text>Hello, {name}</Text>
                </View>
          );


          Greeting.propTypes = {
            name: PropTypes.string
            };

            export default Greeting;
          
   
### Editor Config - Padronização de código
    
  1 - Criar arquivo .editorconfig na raiz do projeto com o seguinto código:
  
  ```
    root = true

    [*]
    indent_style = space
    indent_size = 2
    charset = utf-8
    trim_trailing_whitespace = true
    insert_final_newline = true
  ```
### Reactotron - Ferramenta de Debug

  1 - Instalar o reactotron de acordo com seu OS: 
  * [Reactotron](https://github.com/infinitered/reactotron/releases) - A desktop app for inspecting your React JS and React       Native projects.
  
  2 - Executar o comando no terminal :
  
    ```
      yarn add reactotron-react-native
    ```
  
  3 - Criar pasta config dentro de src;
  
  4 - Criar arquivo ReactotronConfig.js dentro da pasta config com o seguinte conteúdo:
  
    ```
      import Reactotron from 'reactotron-react-native';

      if (__DEV__) {
        const tron = Reactotron.configure()
          .useReactNative() 
          .connect();

        console.tron = tron;
        tron.clear();
      }
    ```
    
  5 - Importar dentro do arquivo src/index.js :
  
      ```
        import './config/ReactotronConfig';

        import React from 'react';
        import { View, Text, StyleSheet } from 'react-native';

        const App = () => (...);
        
        ...
        ...
        ...
      ```
  
  6 - Verificar no aplicativo Reactotron se o App foi identificado;
  
### ESLint - Ferramenta de correção do código (VSCode)

  Antes de continuar instalar as extensões do Prettier e Eslint no VSCode.
  
  Colocar nas configurações do usuário do VSCode as seguinte linhas:
  
      ```
        ...
        "editor.formatOnSave": true,
        "prettier.eslintIntegration": true,
        ...
      ```
  
  1 - Executar comando no terminal:
  
    ```
      yarn add eslint -D
    ```
  2 - Executar comando no terminal: 
  
    ```
      yarn  eslint --init
    ```
    
  3 - Escolher seguintes opções:
  
     ```
       1 - To check syntax, find problems, and enforce code style
       2 - JavaScript modules(import/export)
       3 - React
       4 - Desmarcar Browser e Node com espaço
       5 - Use a popular style guide
       6 - Airbnb
       7 - JSON
       8 - Y enter

     ```
     
   4 - Deletar arquivo criado package-lock.json (Apenas se estiver utilizando yarn );
   
   5 - Executar no terminal  (Apenas se estiver utilizando yarn ):
   
      ```
        yarn
      ```
   
   6 - Executar no terminal:
      ```
      yarn add babel-eslint -D
      ```
   7 - Configurar arquivo .eslintrc.json como a seguir:
   
      ```
              
          {
            "parser": "babel-eslint",
            "env": {
              "es6": true,
              "jest": true
            },
            "extends": ["airbnb", "plugin:react-native/all"],
            "globals": {
              "Atomics": "readonly",
              "SharedArrayBuffer": "readonly",
              "__DEV__": true
            },
            "parserOptions": {
              "ecmaFeatures": {
                "jsx": true
              },
              "ecmaVersion": 2018,
              "sourceType": "module"
            },
            "plugins": ["react", "react-native", "jsx-a11y", "import"],
            "rules": {
              "react/jsx-filename-extension": [
                "error",
                { "extensions": [".js", ".jsx"] }
              ],
              "import/prefer-default-export": "off",
              "no-unused-vars": ["error", { "argsIgnorePattern": "^_" }],
              "react/jsx-one-expression-per-line": "off",
              "react-native/no-color-literals": "off",
              "react-native/sort-styles": "off",
              "global-require": "off"
            },
              "settings": {
              "import/resolver": {
                "babel-plugin-root-import": { "rootPathSuffix": "src" }
              }
            }
          }
      
      ```
      
### Import Resolver - Facilita a importação de arquivos na raiz do projeto, adicionando um prefixo:

   1 - Executar comando no terminal para adicionar o babel plugin root import: 
   
        ```
          yarn add babel-plugin-root-import -D
        ```
   2 - Executar comando no terminal para associar o babel plugin ao eslint: 
   
        ```
          yarn add eslint-plugin-import eslint-import-resolver-babel-plugin-root-import -D
        ``` 
   3 - Configurar o arquivo babel.config.js:
   
        ```
          module.exports = {
          presets: ['module:metro-react-native-babel-preset'],
          plugins: [
            [
              'babel-plugin-root-import',
              {
                rootPathPrefix: '@', // Adicionar o prefixo desejado
                rootPathSuffix: 'src',
              },
            ],
          ],
        };

        ```
   4 - Criar e Configurar o arquivo jsconfig.json para sugestões de importação:
   
        ```
          {
            "compilerOptions": {
              "baseUrl": ".",
              "paths": {
                "@/*": ["src/*"] // Configurar de acord com o prefixo escolhido
              }
            }
          }
        ```
        
### React Dev Tools - Ferramenta para mostrar a árvore de elementos do app

   1 - Instalar a biblioteca react-devtools:
   
   ```
   yarn add react-devtools -D
   ```
   
   2 - Criar o arquivo de configuração DevToolsConfig.js dentro da pasta src/config:
   
   3 - Importar o arquivo dentro do index.js dentro de src
   
   4 - Configurar o arquivo package.json, dentro de scripts, como abaixo:
   
   ```
         ...
              "scripts": {
              "start": "node node_modules/react-native/local-cli/cli.js start",
              "test": "jest",
              "react-devtool": "react-devtools"
            },
        ...
   ```
   
   5 - Acessar a pasta do projeto e rodar o comando yarn run react-devtool
   
   
### Estrutura de pastas e arquivos

```bash
nome-do-projeto
├── src/
│   ├── config/
│   │   └── ReactotronConfig.js
│   │   └── DevToolsConfig.js
│   ├── index.js
├── .buckconfig
├── .editorconfig
├── .eslintrc.json
├── .flowconfig
├── .gitattributes
├── .gitignore
├── .watchmanconfig
├── app.json
├── babel.config.js
├── index.js
├── jsconfig.json
├── metro.config.js
├── package.json
└── yarn.lock
```
   

  

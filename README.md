# init-reactnative

Minha própria configuração para projetos [react-native](https://github.com/facebook/react-native). Caso você queira configurar seu projeto `react-native` com [Typescript](https://github.com/microsoft/TypeScript) e [eslint](https://github.com/eslint/eslint) para facilitar seu desenvolvimento, basta seguir os passos a seguir.

**Segue o preview:**

- [Instalando o react-native](#Instação-do-`react-native`)
- [Configurando hierarquia de pastas](#Configurando-a-hierarquia-de-pastas)
- [Configurando o TypeScript](#TypeScript)
- [Créditos](#Créditos)

* * *

## Instação do `react-native`

O primeiro passo para iniciar um projeto react-native é instalar o pacote global `create-react-native-app` ou um CLI (Interface de linha de comandos) `expo-cli`.

O método utilizado para a criação do projeto `react-native` fornecido pelo próprio [docs](https://reactnative.dev/docs/environment-setup) da biblioteca, é utilizando o `expo-cli`, porém a forma que eu estarei criando será utilizando o `create-react-native-app`.

### Alguns dos gerenciadores de pacotes que podem ser utilizados

1. [Yarn](#Yarn)
2. [Npm](#Npm)

### Yarn

`expo-cli`

```console
~$ yarn global add expo-cli
```

Isso irá instalar globalmente o CLI (Interface de linha de comando) do expo, que poderá ser invocado chamando o comando:

```console
~$ expo ...arguments
```

Para iniciar o projeto com o `expo-cli` você terá que digitar o seguinte comando após a instalação:

```console
~$ expo init projectname
```

Ao chamá-lo dessa forma com o `projectname` que seria o nome de seu projeto ele irá criar uma pasta com o mesmo nome do projeto no local onde você executou o comando. Nesta pasta terá todos os arquivos necessários para você começar a desenvolver.

* * *

`create-react-native-app`

```console
~$ yarn global add create-react-native-app
```

Isso irá instalar o pacote globalmente em seu computador. Sendo possível ser chamado para uso em qualquer linha de comando.

Agora abaixo temos a utilização do pacote que criamos.

```console
~$ create-react-native-app projectname
```

Ao chamar o pacote `create-react-native-app` podemos inserir um nome para ele a frente como argumento ou durante a instalação se não for informado.

### Npm

`expo-cli`

```console
~$ npm install -g expo-cli
```

Você executará os mesmos passos que é mostrado no [Yarn](#Yarn).

* * *

`create-react-native-app`

```console
~$ npm install -g create-react-native projectname
```

Isso irá instalar o pacote globalmente em seu computador. Sendo possível ser chamado para uso em qualquer linha de comando.

Agora abaixo temos a utilização do pacote que criamos.

```console
~$ create-react-native-app projectname
```

Ao chamar o pacote `create-react-native-app` podemos inserir um nome para ele a frente como argumento ou durante a instalação se não for informado.

Caso você prefira criar diretamente o projeto sem a necessidade de digitar os comandos acima, apenas use:

```console
~$ npx create-react-native-app projectname
```

* * *

## Configurando a hierarquia de pastas

As configurações de hierarquia de pastas que utilizo talvez seja "bagunçada", pois existem muitas pastas uma dentro da outras e arquivos talvez desnecessários. Porém a utilizo pensando no projeto, caso ele tenha futuro e possa se tornar um projeto grande, essa estrutura salvaria muito tempo perdido.

Exemplo:

```text
./src/

./src/screens
./src/screens/auth
./src/screens/auth/login
./src/screens/auth/register

./src/components
./src/components/Buttons
./src/components/Buttons/SubmitButton
./src/components/Buttons/LinkButton

./src/assets
./src/assets/images
./src/assets/images/write.svg
./src/assets/images/perfil.jpeg

./src/services
./src/services/api

./src/helpers
./src/helpers/calc
./src/helpers/formatter
```

Existem outras pastas que dependendo do projeto seriam necessárias, porém essas eu utilizo em quase todos os projetos que desenvolvo mesmo que para testes.

Irei tentar resumir a utilização de cada uma:

- `src` - Esta vai ser a *"raiz"* do projeto, onde irá estar os arquivos que iremos criar para dar vida ao nosso aplicativo.

- `screens` - Nesta pasta eu armazeno todas as telas do aplicativo. As telas seriam divididas por sessões. Que no exemplo acima, uma sessão seria o `auth` que seria a sessão de autenticação do aplicativo. Então telas como `login` e `register` seriam inseridas nelas, pois são respectivamente para autenticar o usuário e registrar um novo usuário.

- `components` - Nesta pasta eu armazeno todos os componentes mais *"complexos"* que deixariam o código bagunçado se eu não criasse um modelo para tal.

- `assets` - Nesta pasta eu armazeno todos os assets do aplicativo que ficam do lado do cliente, como imagens, jsons, icónes e outros.

- `services` - Nesta pasta eu armazeno alguns services da aplicação quando necessáraio, um exemplo seria uma requisição para uma api rest.

- `helpers` - Nesta pasta eu armazeno alguns arquivos para ajudar a realizar operações matemáticas ou até formatar valores e textos. No geral seria para ajudar com detalhes pequenos como os citados anteriormente.

*Lembrando que essa hierarquia de pastas é a que eu geralmente utilizo, não é obrigatório ninguém seguir esse padrão. Porém, recomendo utilizarem pelo menos o `./src`.*

* * *

## TypeScript

Agora iremos passar o nosso projeto para `TypeScript`.

Primeiro passo é você passar o arquivo `App.js` para o `./src` com o nome de `App.tsx`, que seria um arquivo `typescript` que permite o uso de `jsx`.

```console
~$ mv App.js ./src/App.tsx
```

Lembre que ao alterar o caminho do componente `App`, você deve ir no `index.js` na raiz do projeto e alterar o caminho do `import`.

Após isso, você deve criar o arquivo `tsconfig.json` na raiz do projeto.

```console
~$ touch tsconfig.json
```

Antes de começar a trabalhar com o `TypeScript` instale as seguintes dependências de desenvolvedor.

### Instalando com `yarn`

```console
~$ yarn add @types/react @types/react-dom @types/react-native typescript -D
```

### Instalando com `npm`

```console
~$ npm install @types/react @types/react-dom @types/react-native typescript --save-dev
```

Agora você deve configurar o seu arquivo de configuração do `TypeScript`. Segue a configuração que utilizo em meu `tsconfig.json` sem o `eslint`.

```json
{
  "compilerOptions": {
    "allowSyntheticDefaultImports": true,
    "jsx": "react-native",
    "lib": ["dom", "esnext"],
    "moduleResolution": "node",
    "noEmit": true,
    "skipLibCheck": true,
    "resolveJsonModule": true,
    "strict": true,
    "baseUrl": ".",
    "paths": {
      "*": ["ts-declarations/*", "node_modules/*"]
    }
  }
}
```

* * *

## Configurando o `eslint`

Agora caso você queira configurar o `tsconfig.json` para trabalhar com o `eslint` basta seguir o processo a seguir.

De início recomendo a instalação da extensão `dbaeumer.vscode-eslint` caso esteja desenvolvendo no `Visual Studio Code`.

Iremos instalar o [CLI](https://eslint.org/docs/user-guide/command-line-interface) do `eslint` para podermos criar com uma maior facilidade os arquivos de configuração do mesmo. Siga os passos a seguir.

### Com `yarn`

Instalando o cli do `eslint`

```console
~$ yarn global add eslint
```

## Com `npm`

Instalando o cli do `eslint`

```console
~$ npm i -g eslint
```

Agora iremos inicializar o assistente de instalação do `eslint`.

```console
~$ eslint --init
```

Após executar este comando, siga os passos a seguir. Lembrando que estas são minhas opções de configurações, caso você queira tentar de outra forma não precisa seguir passo a passo.

### Usando o asistente de configuração

Selecione **"*To check syntax, find problems, and enforce code style*"** para conferir a síntaxe do seu código, procurar erros e também `forçar` um estilo padrão.

```console
? How would you like to use ESLint? ...
  To check syntax only
  To check syntax and find problems
> To check syntax, find problems, and enforce code style
```

Selecione **"*JavaScript modules (import/export)*"** para selecionar o padrão de módulos como `import/export`.

```console
? What type of modules does your project use? ... 
> JavaScript modules (import/export)
  CommonJS (require/exports)
  None of these
```

Selecione **"*React*"** para dizer ao `eslint` que esse é um projeto `react`.

```console
? Which framework does your project use? ...       
> React
  Vue.js
  None of these
```

Selecione **"*Yes*"** para o seu `eslint` configurar automaticamente o `TypeScript` em seu estilo.

```console
? Does your project use TypeScript? » No / Yes
```

Desmarque ambos para que não seja forçado uma configuração baseada em `Node` ou/e `Browser`. Geralmente para projetos `react-native` eu desmarco ambos.

```console
? Where does your code run? ...  (Press <space> to select, <a> to toggle all, <i> to invert selection)
√ Browser
√ Node
```

Aqui vai de pessoa para pessoa, porém eu costumo ir em **"*Use a popular style guide*"**.

```console
? How would you like to define a style for your project? ... 
> Use a popular style guide
  Answer questions about your style
  Inspect your JavaScript file(s)
```

Após ir em **"*Use a popular style guide*"**, sigo para o estilo `Standart`.

```console
? Which style guide do you want to follow? ...
  Airbnb: https://github.com/airbnb/javascript
> Standard: https://github.com/standard/standard        
  Google: https://github.com/google/eslint-config-google
```

Esta última opção não muda muita coisa, é apenas o formato do arquivo de configuração do `eslint`, eu costumo colocar em `JSON`.

```console
? What format do you want your config file to be in? ... 
  JavaScript
  YAML
> JSON
```

Após todo esse processo, irá aparecer uma sequência de dependências a serem instaladas, ele pergunta se você prefere instalar usando `npm`, seleciono `Yes` caso prefira, porém se preferir instalar usando `yarn` ou algum outro gerenciador de pacotes basta copiar toda a sequência de dependências.

A sequência de dependências retornada para mim foi a seguinte:

```console
eslint-plugin-react@latest @typescript-eslint/eslint-plugin@latest eslint-config-standard@latest eslint@^7.12.1 eslint-plugin-import@^2.22.1 eslint-plugin-node@^11.1.0 eslint-plugin-promise@^4.2.1 @typescript-eslint/parser@latest
```

Logo, como pretendo instalar usando `yarn`, basta instalar elas.

```console
~$ yarn add eslint-plugin-react@latest @typescript-eslint/eslint-plugin@latest eslint-config-standard@latest eslint@^7.12.1 eslint-plugin-import@^2.22.1 eslint-plugin-node@^11.1.0 eslint-plugin-promise@^4.2.1 @typescript-eslint/parser@latest -D
```

Após instalar os seguintes pacotes, quase toda a configuração do `eslint` foi feita, o resto seria feita manualmente ou pelo cli do `eslint` de acordo com suas necessidades.

O meu `.eslintrc.json` ficou assim:

```json
{
    "env": {
        "es2021": true
    },
    "extends": [
        "plugin:react/recommended",
        "standard"
    ],
    "parser": "@typescript-eslint/parser",
    "parserOptions": {
        "ecmaFeatures": {
            "jsx": true
        },
        "ecmaVersion": 12,
        "sourceType": "module"
    },
    "plugins": [
        "react",
        "@typescript-eslint"
    ],
    "rules": {
    }
}
```

Porém após modificar de acordo com minhas preferências, o resultado do arquivo `.eslintrc.json` final ficou assim:

```json
{
    "env": {
        "es2021": true
    },
    "extends": [
        "plugin:react/recommended",
        "standard",
        "prettier",
        "prettier/react",
        "prettier/@typescript-eslint",
        "plugin:prettier/recommended"
    ],
    "parser": "@typescript-eslint/parser",
    "parserOptions": {
        "ecmaFeatures": {
            "jsx": true
        },
        "ecmaVersion": 12,
        "sourceType": "module"
    },
    "plugins": [
        "react",
        "@typescript-eslint",
        "prettier"
    ],
    "rules": {
        "import/no-unresolved": 0,
        "react/jsx-filename-extension": [1, {
        "extensions": [
            ".ts",
            ".tsx"
        ]
        }],
        "prettier/prettier": [
            "error",
            {
                "singleQuote": true,
                "trailingComma": "all",
                "arrowParens": "avoid",
                "endOfLine": "auto",
                "semi": false
            }
        ],
        "no-use-before-define": "off"
    },
    "overrides": [
        {
            "files": [
                "__tests__/*.js"
            ],
            "rules": {
                "react/jsx-filename-extension": "off"
            },
            "env": {
                "jest": true
            }
        }
    ]
}
```

Caso esteja interessado nesta configuração, basta realizar a instalação do `prettier`, `eslint-config-prettier` e `eslint-plugin-prettier` como dependência de desenvolvedor. Em seguida deve substituir as diferenças de meu arquivo `.eslintrc.json` para o seu arquivo.

### Pelo `yarn`

```console
~$ yarn add prettier eslint-config-prettier eslint-plugin-prettier -D
```

### Pelo `npm`

```console
~$ npm install prettier eslint-config-prettier eslint-plugin-prettier --save-dev
```

Também recomendo vocês terem as seguintes configurações em seu `settings.json` do `vscode`

```json
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
      "source.fixAll": true,
      "source.fixAll.eslint": true
  },
  "eslint.validate": [
      "javascript",
      "javascriptreact",
      "typescript",
      "typescriptreact"
  ],
```

* * *

## Executando projeto

Para executar um projeto `react-native` você deve olhar como é chamado os scripts no arquivo `package.json`, os meus por exemplo são:

```json
  "scripts": {
    "android": "react-native run-android",
    "ios": "react-native run-ios",
    "web": "expo start --web",
    "start": "react-native start",
    "test": "jest"
  },
```

Agora basta você executar algum `script` referente ao que você procura. Caso queira executar pelo expo, basta instalar o `expo-cli` e executar o seguinte:

```console
~$ expo start
```

Isso irá abrir o servidor de desenvolvimento do `expo`.

Para mais informações acesse: [expo starting the development server](https://docs.expo.io/get-started/create-a-new-app/#starting-the-development-server)

* * *

## Créditos

### Oeee 😊, prazer sou o Vinícius mas pode me chamar de [sydo26](https://github.com/sydo26)

Sou quem criou esse `"mini-tutorial"` sobre como iniciar um projeto `react-native` com um ambiente de desenvolvimento confortável. Meu intuito com esse tutorial foi criar tanto um `padrão` para eu mesmo seguir e também ajudar a comunidade que está iniciando nesse grande mundo.

Pretendo fazer mais tutoriais neste mesmo repositório, porém isso é algo que irei fazer mais para frente. De qualquer forma espero que eu tenha conseguido ajudar algúem 😃.

### Redes sociais

[Instagram](https://www.instagram.com/sydo26/)
[Twitter](https://twitter.com/sydo26)
[Linkedin](https://www.linkedin.com/in/sydo26/)

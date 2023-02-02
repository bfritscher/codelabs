summary: Getting Started with Vue.js Project Setup
id: vue-dev-setup
categories: Web
tags: vuejs
status: Published 
authors: Boris Fritscher
feedback link: https://github.com/bfritscher/cours-pweb-slides

# Getting Started with Vue.js Project Setup


## Getting Started

In this lab we will setup a new local Vue.js project with the Vite build tool.

<aside class="negative">
Older version of Vue used Vue CLI, but this is no longer recommended.
</aside>

<aside class="positive">
Looking for more? More details in the official <a href="https://vuejs.org/guide/quick-start.html">Vue.js Guide</a>
</aside>


## Install Development Environment Prerequisites

Download and install [Node.js](https://nodejs.org/) to get `npm`.

Download and install [Git](https://git-scm.com/download/win) to get `git`.

Download and install [Visual Studio Code](https://code.visualstudio.com/) to get `code`.


Check that it works from the shell:

```sh
$ git --version
git version X.Y.Z

$ node --version
vX.Y.Z

$ code --version
X.Y.Z
...
x64
```



## Create a new project

First change to a parent folder in which the project folder will be created.


Use vue/vite to create a new project.

```sh
C:\temp> npm init vue@latest
```

![](assets/vue-create.png)





## Install Extensions for VS Code

Change into the directory and launch vscode
```sh
$ cd labo-vue
$ code .
```

- install [vscode Vue Volar extension](vscode:extension/Vue.volar)
- install [vscode Prettier extension](vscode:extension/esbenp.prettier-vscode)
- install [vscode eslint extension](vscode:extension/dbaeumer.vscode-eslint)

- install [vue chrome devtool extension](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd)



## Install Project Dependencies

Must be done inside the project's root folder!

```sh
$ npm install
```

This will read `package.json` and update `node_modules` folder.



## Preview Your App in The Browser


Start the development server
```sh
npm run dev
```

edit a file and watch livereload in action.

For example add `<h1>Test vue!</h1>` to `<body>` in `./index.html`.


Stop the server with `ctrl+c`




## Cleanup

- Delete `src/assets/base.css`
- Empty  `src/assets/main.css`
- Replace `src/App.vue` with this code:

```html
<template>
  <div class="container">
    <h1>Hello Bootstrap</h1>
    <div class="row">
      <div class="col-sm">
        <button class="btn btn-primary">{{ message }}</button>
      </div>
      <div class="col-sm">
        <i class="fas fa-ice-cream display-1 text-primary"></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: "Hello Vue!",
    };
  },
};
</script>

<style></style>
```

## Add Bootstrap and Font Awesome

Check package.json (before and after)

1. Add dependencies

```sh
$ npm install --save bootstrap @popperjs/core
$ npm install --save @fortawesome/fontawesome-free
```


2. Inside `src/main.js` add imports

```javascript
import "bootstrap";
import "bootstrap/dist/css/bootstrap.min.css";
import "@fortawesome/fontawesome-free/css/all.min.css";
```



## Try More Font Awesome

Check that the icon works:

<svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="ice-cream" class="svg-inline--fa fa-ice-cream fa-w-14" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="#dc3545" d="M368 160h-.94a144 144 0 1 0-286.12 0H80a48 48 0 0 0 0 96h288a48 48 0 0 0 0-96zM195.38 493.69a31.52 31.52 0 0 0 57.24 0L352 288H96z"></path></svg>



Add another icon to the `App.vue template inside the button`

https://fontawesome.com/icons

```html
<i class="fa-solid fa-cake-candles"></i>
```



## Use npm to install other packages

Lets try another bootstrap look.

```sh
npm install bootswatch --save
```

https://bootswatch.com/

try different CSS files from bootswatch in `main.js`

```javascript
import "bootswatch/dist/darkly/bootstrap.min.css";
```


## Test linting

We installed two linter:

- Prettier for code formatting
- ESLint for code quality

Run the command and check how the files are changed.

```sh
$ npm run lint
```

Copy this line into main.js and see what happens.

```js
let myvar = 'Hello World'
```

Check the PROBLEMS tab of vscode
(right-click to fix problem).


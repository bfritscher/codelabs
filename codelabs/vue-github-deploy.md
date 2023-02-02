summary: Deploying a Vue.js Project on GitHub
id: vue-github-deploy
categories: Web
tags: vuejs
status: Published 
authors: Boris Fritscher
feedback link: https://github.com/bfritscher/cours-pweb-slides

# Deploying a Vue.js Project on GitHub


# Lab 2: deploy to github pages

![](images/yeoman-ship.png)<!-- .element: class="w-30" -->



### Step 0: Install

Create a [github.com](https://github.com) account and install [git-scm.com](https://git-scm.com/download/win) to have a version of `git`.



### Step 0: Use LF also on windows

Create `.gitattributes` with content:

```txt
# Force all line endings to be \n
* text eol=lf

############################################################
# git can corrupt binary files if they're not set to binary.
############################################################

# Apple office documents are actually folders, so treat them as binary.
*.numbers binary
*.pages binary
*.keynote binary

# Image files
*.png binary
*.jpg binary
*.jpeg binary
*.gif binary
*.webp binary
*.ico binary

# Movie and audio files
*.mov binary
*.mp4 binary
*.mp3 binary
*.flv binary
*.ogg binary

# Compression formats
*.gz binary
*.bz2 binary
*.7z binary
*.zip binary

# Web fonts
*.ttf binary
*.eot binary
*.woff binary
*.otf binary

# Other
*.fla binary
*.swf binary
*.pdf binary

############################################################
# End binary settings
############################################################
```



### Step 1: Git Main

- Create github repository [labo-xyz](https://classroom.github.com/a/KHAPN3aT)
- Init a git repository
- Add and Commit your code.
- Add remote
- Push your code to Github.



### Step 2: Production version test

Create a built, mimified version of your page with your .
```sh
npm run build
```
*Notice that you have a dist folder with this new content.*

Test production version with:
```sh
npm run preview
```



### Step 3: Deploy static site on Github

Github offers to serve static web pages https://pages.github.com/

There are two options:

- User site: http://usernameABC.github.io by creating a special repository with the name: usernameABC.github.io
- Projet site: http://usernameABC.github.io/repositoryYXZ by creating a special branch gh-pages inside the repositoryXYZ


Note:

A special CNAME file can be put at the root of gh-pages to use a custom domain name.



## Setup Github and gh-pages via Github Actions

- configure github Actions to build and deploy to gh-pages
- configure vue to support /labo-xyz/ in production
- commit and push



### Github Action Config

- create folder `.github\workflows`
- add this file `build_deploy.yml`

```yml
name: Build and Deploy to GH-Pages

on:
  push:
    branches:
      - master
      - main

jobs:
  build_deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v2

      - name: Setup Node
        uses: actions/setup-node@v2
        with:
          node-version: '16'

      - name: Cache dependencies
        uses: actions/cache@v2
        with:
          path: ~/.npm
          key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
          restore-keys: |
            ${{ runner.os }}-node-
      - run: npm ci
      #- run: npm test
      - run: npm run build

      - name: deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist

```



### Configure Vite publicPath
Edit `vite.config.js` file to handle subfolder deployment.
```sh
export default defineConfig({
  ...,
  base: process.env.NODE_ENV === "production" ? "/labo-test/" : "/",
});
```



### Try to deploy

After a successful ```npm run build``` commit all changes and push:
```sh
git add . --all
git commit
git push
```

The site can be accessed at: https://heg-web.github.io/labo-test/ when action workflow is finished.

<!-- .element: class="small" -->



### You did it!

Your First Single Page Web Application is deployed in Production!

![](assets/youdidit.gif)



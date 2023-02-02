summary: Deploying a Vue.js Project on GitHub
id: vue-github-deploy
categories: Web
tags: vuejs
status: Published
authors: Boris Fritscher
feedback link: https://github.com/bfritscher/cours-pweb-slides

# Deploying a Vue.js Project on GitHub Pages

## Getting Started

We want to use the static hosting services offered by [github.com](https://github.com). In addition, we will also use their server-side actions to build the project before deploying it automatically on each commit.

1. Create a [github.com](https://github.com) account.
2. Install [git-scm](https://git-scm.com/download/) to have a version of `git`.


## Use LF also on windows

We want to work with LF line endings instead of CRLF.

Create `.gitattributes` at the root of your project with the following content:

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



## Git Repositry

Use git to create a local repostiory and connect it to a github online repository.

<aside class="positive">
Looking for more? Checkout <a href="https://bfritscher.github.io/cours-git-slides/#/">GIT Workshop<a> or <a href="https://git-scm.com/doc">git documentation</a>
</aside>


1. Create a github repository
2. Init a local git repository
3. Add and Commit your code
4. Add the github remote
5. Push your code to Github.

<aside class="negative">
You <b>must</b> have at least one commit to be able to push!
</aside>


## Test Production Version

The first time or to debug something without sending multiple commits to gihub you should first try to build your project at least once locally.

### Create a built, mimified version of your page with:
```sh
npm run build
```
*Notice that you have a new `dist/` folder with this new content.*

### Test production version with this command:
```sh
npm run preview
```
This will start a webserver serving the files in the dist folder.


## Deploy static site on Github

Github offers to serve static web pages [https://pages.github.com/](https://pages.github.com/)

There are two options:

- User site: http://usernameABC.github.io by creating a special repository with the name: usernameABC.github.io
- Projet site: http://usernameABC.github.io/repositoryYXZ by creating a special branch gh-pages inside the repositoryXYZ


<aside class="positive">
A special CNAME file can be put at the root of gh-pages to use a custom domain name.
</aside>


### Setup Github and gh-pages via Github Actions

- configure github Actions to build and deploy to gh-pages
- configure vue to support /subfolder-repository-name/ in production
- commit and push



## Github Action Config

### Create folder `.github\workflows`
```txt
Project
 |
 |-- .github
        |
        |-- workflows
               |
               |-- build_deploy.yml

```

### Add this file `build_deploy.yml`
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



## Configure Vite publicPath

### Edit `vite.config.js` file to handle subfolder deployment.
```sh
export default defineConfig({
  ...,
  base: process.env.NODE_ENV === "production" ? "/labo-test/" : "/",
});
```

<aside class="negative">
Make sure to adapt the code to <b>your</b> configuration.
</aside>


## Try to deploy

After a successful ```npm run build``` commit all changes and push:
```sh
git add . --all
git commit
git push
```

The site can be accessed at: https://heg-web.github.io/labo-test/ when action workflow is finished.




## You did it!

Your First Single Page Web Application is deployed in Production!

![](assets/youdidit.gif)



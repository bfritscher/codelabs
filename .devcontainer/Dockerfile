# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.140.1/containers/javascript-node/.devcontainer/base.Dockerfile

# [Choice] Node.js version: 14, 12, 10
ARG VARIANT="14"
FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:0-${VARIANT}

# ENV PATH="$PATH:/usr/local/go/bin:/home/node/go/bin"

EXPOSE 8000

RUN curl -sL  $(curl -s https://api.github.com/repos/bfritscher/codelabs-tools/releases/latest | grep browser_download_url | cut -d\" -f4 | grep 'claat-linux-amd64') -o /usr/local/bin/claat && chmod 755 /usr/local/bin/claat

# [Optional] Uncomment this section to install additional OS packages.
# RUN wget https://go.dev/dl/go1.20.linux-amd64.tar.gz \
#    && tar -C /usr/local -xzf go1.20.linux-amd64.tar.gz \
#    && rm go1.20.linux-amd64.tar.gz

# RUN su node -c "/usr/local/go/bin/go install github.com/bfritscher/codelabs-tools/claat@latest"
RUN sudo -u node npm install -g gulp-cli nodemon
# [Optional] Uncomment if you want to install an additional version of node using nvm
# ARG EXTRA_NODE_VERSION=10
# RUN su node -c "source /usr/local/share/nvm/nvm.sh && nvm install ${EXTRA_NODE_VERSION}"

# [Optional] Uncomment if you want to install more global node modules
# RUN sudo -u node npm install -g <your-package-list-here>

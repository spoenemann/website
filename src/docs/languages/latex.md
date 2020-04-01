# LaTeX in Gitpod

This tutorial will demonstrate how to configure Gitpod to work with [LaTeX](https://www.latex-project.org/) files. You can find a complete [example repository](https://github.com/ptrottier/latex) at the end.

## Installing LaTeX

First, you'll probably want to install LaTeX in Gitpod. To do this, add a new file to your repository called [.gitpod.Dockerfile](https://www.gitpod.io/docs/config-docker/), and add the following content to it:

```Dockerfile
FROM gitpod/workspace-full

# Install LaTeX
RUN sudo apt-get -q update && \
    sudo apt-get install -yq texlive-full && \
    sudo rm -rf /var/lib/apt/lists/*
```

Additionally create a file called [.gitpod.yml](https://www.gitpod.io/docs/config-gitpod-file/) and add the following:

```YAML
image:
  file: .gitpod.Dockerfile
```

Now commit both files into source control, and push them to your GitHub or GitLab repository.

This will be your base configuration for LaTeX in Gitpod: From now on, every time you open a new Gitpod workspace for your repository, it will be configured as specified in your `.gitpod.yml` and `.gitpod.Dockerfile`.

## Automatically compiling LaTeX files on save

Install `inotify-tools` by modifying your earlier `.gitpod.Dockerfile` like so:

```Dockerfile
FROM gitpod/workspace-full

# Install LaTeX
RUN sudo apt-get -q update && \
    sudo apt-get install -yq texlive-full inotify-tools && \
    sudo rm -rf /var/lib/apt/lists/*
```

Next modify your `.gitpod.yml` like so:

```YAML
image:
  file: .gitpod.Dockerfile

tasks:
  - name: LaTeX auto-rebuild
    command: >
      while find . -name '*.tex' | xargs inotifywait -qqre modify .; do \
        latexmk -pdf ; \
      done
  - name: Terminal
```

## VSCode Extensions

### TexLab

This extension provides rich editing support for the LaTeX typesetting system powered by the [TexLab](https://github.com/latex-lsp/texlab) language server.

```yml
vscode:
  extensions:
    - efoerster.texlab@1.10.0:/Vq+k9Ug/81LYWajjTgMpA==
```

## Try it!

To see a complete minimal example repository with a Gitpod configuration for LaTeX, including all the tools we've covered, see [ptrottier/latex](https://github.com/ptrottier/latex). You can try it in your browser:

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/ptrottier/latex)

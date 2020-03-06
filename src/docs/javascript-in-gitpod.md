# JavaScript in Gitpod

Gitpod comes with great support for JavaScript built-in and tools like Node, npm and yarn pre-installed. Still depending on your project you might want to further optimize the experience.

## Examples

Here are a few JavaScript example projects that are automated with Gitpod:

Repository | Description | Try it
---|---|---
[Mozilla pdf.js](https://github.com/mozilla/pdf.js) | PDF.js is a Portable Document Format (PDF) viewer that is built with HTML5. | [![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/mozilla/pdf.js)
[Tesseract.js](https://github.com/naptha/tesseract.js) | Pure Javascript OCR for more than 100 Languages. | [![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/naptha/tesseract.js)

## Start tasks

Almost the entirety of JavaScript projects nowadays have some sort of build tool for things like bundling, linting, code-splitting and so on and they also use some sort of package manager either it be npm or yarn for managing dependecies. 

You can pre-install dependecies and run tasks like `build`, `lint`, `test` and so on even before you start a workspace for doing so please create a `.gitpod.yml` file in the root of your project and add the tasks depending on your project needs. An example might look like this:

```yaml
tasks:
    - init: npm install && npm run prod
      command: npm run dev
```

you can read more about tasks [here](/docs/config-start-tasks/). 

## Node Versions

Gitpod comes with node version 10.19.0 pre-installed but let say your projects uses a different version of node well the good news it that Gitpod also comes with nvm(a tool used to manage multiple active Node. js versions) installed. To install and configure the desired version you can use the following in a terminal:

```bash
nvm install 12.0
nvm use 12.0
```

## Using Eslint for linting

If your project's `package.json` does not mentions Eslint as a dependency then you have to first install it via:

```bash
npm install -g eslint
```

and then add the following to your .gitpod.yml:

```yaml
vscode:
  extensions:
    - dbaeumer.vscode-eslint@2.0.15:/v3eRFwBI38JLZJv5ExY5g==
```

Also if you don't want to re-install the eslint package whenever you open a new workspace you can append  `npm install -g eslint` to the end of your `init` task in `.gitpod.yml`:

```yaml
tasks:
    - init: npm install && npm run prod && npm install && npm install -g eslint
```



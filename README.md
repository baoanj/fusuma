<div align="center">
  <h1>Fusuma</h1>
</div>

<div align="center">
  <strong>📝 Make slides with Markdown easily.</strong>
</div>

<br />

Just write MarkDown and create cool slides.😎

## Run

```sh
$ yarn          # install fusuma
$ yarn start    # development localhost:8080
$ yarn build    # build as NODE_ENV=production
$ yarn deploy   # deploy to github pages
$ yarn pdf      # export as PDF from HTML
```

## Features

- supports [WebSlides](https://webslides.tv)
- supports [Presentation API](https://developer.mozilla.org/en-US/docs/Web/API/Presentation_API)
  - also, it works even without Presentation API
- supports various modes
  - development
  - production build
  - exporting as PDF
  - deploying to GitHub Pages
- supports SNS, OGP, FullScreen, and etc...
- supports Presenter Mode
  - you can give a speech while watching a presenter's notes and a timer
- customizes JavaScript and CSS freely

## Demos

- [introduction slide of Fusuma](https://hiroppy.github.io/fusuma/intro) [[repository](https://github.com/hiroppy/fusuma/samples/intro)]
- others [[repository](https://github.com/hiroppy/slides#my-slides)]

You can also try Fusuma in Gitpod, a one-click online IDE for GitHub:

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/hiroppy/fusuma/blob/master/samples/intro/slides/0-title.md)

## Install

Node versions > v8

```sh
$ npm i fusuma --save-dev # or npm i fusuma -g

# if you want to use yarn
$ yarn add fusuma --dev
```

## Procedure

Just execute the following three lines for executing, generating and deploying slides!

```sh
$ npm i fusuma -D
$ npx fusuma init
$ mkdir slides && echo '# Hello😄' > slides/title.md

# --- Tree ---
$ tree -a
.
├── .fusumarc.yml
└── slides
    └── title.md

1 directory, 2 files

# --- executable tasks---
$ npx fusuma start    # development
$ npx fusuma build    # build as NODE_ENV=production
$ npx fusuma deploy   # deploy to github pages
$ npx fusuma pdf      # export as PDF from HTML
```

When `npx fusuma start` is executed, fusuma will create a slide as follows and serves localhost:8080.

And you can customize the slide using CSS.

## Directory Structure

Please see [samples/intro](https://github.com/hiroppy/fusuma/samples/intro) or [Verification Repository](https://github.com/issue-verifier/fusuma).

Slide order is numeric, alphabetical.

```
.
├── .fusumarc.yml       <-- the configuration file
├── index.js            <-- optional for rewriting
├── slides              <-- slides written by Markdown or HTML
│   ├── 0-title.md
│   ├── 01-content.md
│   ├── 02-body
│   │   └── 0-title.md
│   └── 03-end.md
└── style.css           <-- optional for rewriting

2 directories, 7 files
```

Or slides can be divided by `---` like below.

```markdown
## Hello

This is the first slide.

---

## 🤭

This is the second slide.
```

## Usage

Fusuma provides CLI.

```sh
   fusuma.js 1.0.0 - CLI for easily make slides with Markdown

   USAGE

     fusuma.js <command> [options]

   COMMANDS

     init                Create a configure file
     start               Start with webpack-dev-server
     build               Build with webpack
     deploy              Deploy to GitHub pages
     pdf                 Export as PDF
     help <command>      Display help for a specific command

   GLOBAL OPTIONS

     -h, --help         Display help
     -V, --version      Display version
     --no-color         Disable colors
     --quiet            Quiet mode - only displays warn and error messages
     -v, --verbose      Verbose mode - will also output debug messages
```

## Configuration File

Supports for `yaml` and `js` and it can be generated by running `fusuma init`.

### .fusumarc.yml

<details>

```yaml
meta:
  url: https://slides.hiroppy.me
  name: the present and future of JavaScript
  author: Yuta Hiroto
  description: Explain how specifications are determined and how it will be in the future.
  thumbnail: https://avatars1.githubusercontent.com/u/1725583?v=4&s=200
  siteName: slides.hiroppy.me
  repositoryUrl: https://github.com/hiroppy/fusuma
  sns:
    - twitter
    - hatena
slide:
  loop: true
  sidebar: true
  targetBlank: true
  showIndex: false
  isVertical: false
  code:
    languages:
      - javascript
    plugins:
      - line-numbers
    theme: default
extends:
  js: index.js
  css: style.css
```

</details>

### .fusumarc.js

<details>

```js
module.exports = {
  meta: {
    url: 'https://slide.hiroppy.me',
    name: 'test-test',
    author: 'hiroppy',
    description: 'test',
    thumbnail: 'url',
    siteName: 'siteName',
    sns: ['twitter', 'hatena'],
    repositoryUrl: 'https://github.com/hiroppy/fusuma'
  },
  slide: {
    loop: true,
    sidebar: true,
    targetBlank: true,
    showIndex: false,
    isVertical: false,
    code: {
      languages: ['javascript'],
      plugins: ['line-numbers'],
      theme: 'default'
    }
  },
  extends: {
    js: 'index.js',
    css: 'style.css'
  }
};
```

</details>

## Slide Syntax

See the example slide:) [Syntax Provided by Fusuma](https://github.com/hiroppy/fusuma/samples/intro/slides/04-slide.md)

## Code Syntax Highlighting

Fusuma uses [Prism.js](https://prismjs.com/).  
You can specify `languages`, `plugins`, `theme` to `.fusumrc`.
Please see [babel-plugin-prismjs](https://github.com/mAAdhaTTah/babel-plugin-prismjs) for detail.

```yml
slide:
  code:
    languages: # the default is ['javascript']
      - javascript
    plugins: # the default is []
      - line-numbers
    theme: default # the default is "default"
```

[Playground of Prism.js](https://prismjs.com/test.html#language=markup)

## Presenter Mode

1. open Sidebar(click the bottom right button(三))
2. click the PC monitor icon
3. if you use Chrome, you can choose select cast device
4. if you use a browser that does not support Presentation API, a new window will be created

## API

```js
const { start, build, deploy, pdf } = require('fusuma');
```

<h1 align="center">
  <br>
  <img src="assets/logo.png" width="300" height="69">
</h1>

<p align="center"><strong>An extremely fast and lightweight glob-matching library for JavaScript</strong></p>

<p align="center">
  <a href="https://www.npmjs.com/package/outmatch"><img src="https://img.shields.io/npm/v/outmatch" alt="npm package"></a>
  &nbsp;
  <a href="https://github.com/axtgr/outmatch/actions"><img src="https://img.shields.io/github/workflow/status/axtgr/outmatch/CI?label=CI&logo=github" alt="CI"></a>
  &nbsp;
  <a href="https://www.buymeacoffee.com/axtgr"><img src="https://img.shields.io/badge/%F0%9F%8D%BA-Buy%20me%20a%20beer-red?style=flat" alt="Buy me a beer"></a>
</p>

<br>

Outmatch takes one or more glob patterns, compiles them into a RegExp and returns a function for matching strings with it.

```js
import outmatch from "outmatch";

const isMatch = outmatch("src/**/*.{js,ts}");

isMatch("src/components/header/index.js"); //=> true
isMatch("src/README.md"); //=> false
```

## Why outmatch?

<table>
  <tr>
    <td align="center">💪</td>
    <td><b>Powerful</b><br>Supports basic and extended matching as well as custom path separators, which are a unique feature of this library</td>
  </tr>
  <tr>
    <td align="center">🏎</td>
    <td><b>Fast</b><br>Compiles and matches patterns faster than minimatch, micromatch and picomatch</td>
  </tr>
  <tr>
    <td align="center">🍃</td>
    <td><b>Lightweight</b><br>No dependencies. Just 1.8 KB when minified and gzipped</td>
  </tr>
  <tr>
    <td align="center">⚒</td>
    <td><b>Reliable</b><br>Written in TypeScript, covered by thousands of unit tests</td>
  </tr>
  <tr>
    <td align="center">🌞</td>
    <td><b>Simple</b><br>The API is a single function. Options can be specified in easy to understand language rather than Linux slang</td>
  </tr>
  <tr>
    <td align="center">🔌</td>
    <td><b>Compatible</b><br>Works in any ES5 environment without transpilation</td>
  </tr>
</table>

## Install

Outmatch is distributed via the [npm package registry](https://www.npmjs.com/). It can be installed using one of the compatible package managers or included directly from a CDN.

#### [npm](https://www.npmjs.com/)

```
npm install outmatch
```

#### [Yarn](https://yarnpkg.com/)

```
yarn add outmatch
```

#### [pnpm](https://pnpm.js.org/)

```
pnpm install outmatch
```

#### CDN

- [jsDelivr](https://www.jsdelivr.com/package/npm/outmatch)
- [unpkg](https://unpkg.com/outmatch)

## License

[ISC](LICENSE)

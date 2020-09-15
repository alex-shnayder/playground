<h1 align="center">Outmatch</h1>

<p align="center">An extremely fast and lightweight glob-matching library for JavaScript</p>

<p align="center">
  <a href="https://www.npmjs.com/package/outmatch"><img src="https://img.shields.io/npm/v/outmatch" alt="npm package"></a>
  &nbsp;
  <a href="https://github.com/axtgr/outmatch/actions"><img src="https://img.shields.io/github/workflow/status/axtgr/outmatch/CI?label=CI&logo=github" alt="CI"></a>
  &nbsp;
  <a href="https://www.buymeacoffee.com/axtgr"><img src="https://img.shields.io/badge/%F0%9F%8D%BA-Buy%20me%20a%20beer-red?style=flat" alt="Buy me a beer"></a>
</p>



Outmatch takes one or more glob patterns, compiles them into a RegExp and returns a function for matching strings with it.

```js
import outmatch from 'outmatch'

const isMatch = outmatch('src/**/*.{js,ts}')

isMatch('src/components/header/index.js') //=> true
isMatch('src/README.md') //=> false
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

`npm install outmatch`

## License

[ISC](LICENSE)

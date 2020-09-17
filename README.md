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

Glob patterns are strings that contain wildcards such as `*`, `?`, `[abc]` and others. When a pattern is matched with another string, these wildcards can replace one or more symbols. For example, `src/*` would match both `src/foo` and `src/bar`.

While globs are usually used to search file paths separated by slashes, with outmatch it is possible to match _arbitrary_ strings, whether separated or not.

## Quickstart

```
npm install outmatch
```

```js
import outmatch from 'outmatch'

const isMatch = outmatch('src/**/*.{js,ts}')

isMatch('src/components/header/index.js') //=> true
isMatch('src/README.md') //=> false

isMatch.regExp //=> /^(src((?!\.) ... ((?!).)*\.ts)$/
isMatch.pattern //=> 'src/**/*.{js,ts}'
isMatch.options //=> { separator: true }
```

More details are available in the [Installation](#installation) and [Usage](#usage) sections.

## Why outmatch?

<table>
  <tr>
    <td align="center">💪</td>
    <td><b>Powerful</b><br>Supports extended globbing, brace expansion, multi-pattern compilation and custom path separators, which are a unique feature of this library</td>
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

For detailed comparison with the alternatives, see the [corresponding section](#comparison).

## Installation

Outmatch is distributed via the npm package registry. It can be installed using one of the compatible package managers or included directly from a CDN.

#### [npm](https://www.npmjs.com)

```
npm install outmatch
```

#### [Yarn](https://yarnpkg.com)

```
yarn add outmatch
```

#### [pnpm](https://pnpm.js.org)

```
pnpm install outmatch
```

#### CDN

- [jsDelivr](https://www.jsdelivr.com/package/npm/outmatch)
- [unpkg](https://unpkg.com/outmatch)

## Syntax

### Basic wildcards

Wildcard | Description
-------- | ------------
`?`      | Matches exactly one arbitrary character (excluding separators if specified in options)
`*`      | Matches zero or more arbitrary characters (excluding separators if specified in options)
`**`     | Has a special meaning only if the `separator` property in options is not `false`. Matches any number of segments when used as a whole segment (`/**/` in the middle, `**/` at the beginning or `/**` at the end of a separated string)

### Character Classes

Character classes are defined by one or more symbols surrounded by square brackets. One class always matches exactly one character.

Class                | Matches                                                                                                                                        | Description
-------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | -----------
`[a2_]`              | `a`,&nbsp;`2`,&nbsp;`_`                                                                                                                        | If there are multiple characters in brackets, the class will match any single character from the specified list
`[a-z]`<br>`[0-9]`   | any&nbsp;letter&nbsp;from&nbsp;`a`&nbsp;to&nbsp;`z`<br>any&nbsp;number&nbsp;from&nbsp;`0`&nbsp;to&nbsp;`9`                                     | If two characters in brackets are separated by a hyphen, the class will match any single character from the specified range
`[!abc]`<br>`[!f-k]` | any&nbsp;character&nbsp;except&nbsp;`a`,&nbsp;`b`,&nbsp;`c`<br>any&nbsp;character&nbsp;except&nbsp;letters&nbsp;from&nbsp;`f`&nbsp;to&nbsp;`k` | If the first character in brackets is an exclamation mark, the class will match any single character _not_ in the list or range

### Extglobs

Extended glob patterns represent a choice of alternatives repeated a certain number of times.

Extglob                   | Matches                                                                                                        | Description
------------------------- | ---------------------------------------------------------------------------------------------------------------| -----------
`@(bar\|baz)`             | `bar`,&nbsp;`baz`                                                                                              | One of the given subpatterns exactly one time
`?(foo)`<br>`?(bar\|baz)` | empty&nbsp;string,&nbsp;`foo`<br>empty&nbsp;string,&nbsp;`bar`,&nbsp;`baz`                                     | One of the given subpatterns zero or one time 
`*(foo)`<br>`*(bar\|baz)` | empty&nbsp;string,&nbsp;`foo`,&nbsp;`foofoofoo`<br>empty&nbsp;string,&nbsp;`bar`,&nbsp;`bazbaz`,&nbsp;`barbaz` | One of the given subpatterns zero or more times
`+(foo)`<br>`+(bar\|baz)` | `foo`,&nbsp;`foofoofoo`<br>`bar`,&nbsp;`bazbaz`,&nbsp;`barbaz`                                                 | One of the given subpatterns one or more times
`!(foo)`<br>`!(bar\|baz)` | any&nbsp;string&nbsp;except&nbsp;`foo`<br>any&nbsp;string&nbsp;except&nbsp;`bar`,&nbsp;`baz`                   | Anything except for the given subpatterns

### Braces

### Escaping

Any special character can be escaped by preceding it with a backslash (`\\`).

### Negation

## Comparison

Coming soon.

## License

[ISC](LICENSE)

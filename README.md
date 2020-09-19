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

## Usage

### Separators


### Syntax

<table>
  <tr>
    <th>Pattern</th>
    <th>Matches</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>?</code></td>    
    <td></td>
    <td>Matches exactly one arbitrary character excluding separators</td>
  </tr>  
  <tr>
    <td><code>*</code></td>    
    <td></td>
    <td>Matches zero or more arbitrary characters excluding separators</td>
  </tr>  
  <tr>
    <td colspan="3"><strong>Globstar</strong><br>If the `separator` option is not `false` and a pattern contains separators, two consecutive stars have a special meaning when they are used as a whole segment (e.g. `/**/` if `/` is the separator)</td>
  </tr>
  <tr>
    <td><code>**</code></td>    
    <td></td>
    <td>Matches any number of segments when used as a whole segment in a separated pattern</td>
  </tr>
  <tr>
    <td colspan="3"><strong>Character classes</strong><br>Represent a single character defined by a sequence or range of characters in square brackets</td>
  </tr>
  <tr>
    <td><code>[abc1_]</code></td>
    <td><code>a</code>,&nbsp;<code>b</code>,&nbsp;<code>c</code>,&nbsp;<code>2</code>,&nbsp;<code>_</code></td>
    <td>If there are multiple characters in brackets, the class will match any single character from the specified list</td>
  </tr>  
  <tr>
    <td><code>[a-z]</code><br><code>[0-9]</code></td>
    <td>any&nbsp;letter&nbsp;from&nbsp;<code>a</code>&nbsp;to&nbsp;<code>z</code><br>any&nbsp;number&nbsp;from&nbsp;<code>0</code>&nbsp;to&nbsp;<code>9</code></td>
    <td>If two characters in brackets are separated by a hyphen, the class will match any single character from the specified range</td>
  </tr>  
  <tr>
    <td><code>[!abc]</code><br><code>[!f-k]</code></td>
    <td>any&nbsp;character&nbsp;except&nbsp;<code>a</code>,&nbsp;<code>b</code>,&nbsp;<code>c</code><br>any&nbsp;character&nbsp;except&nbsp;letters&nbsp;from&nbsp;<code>f</code>&nbsp;to&nbsp;<code>k</code></td>
    <td>If the first character in brackets is an exclamation mark, the class will match any single character _not_ in the list or range</td>
  </tr> 
  <tr>
    <td colspan="3"><strong>Extglobs</strong><br>Extended glob patterns represent a choice of alternatives repeated a certain number of times.</td>
  </tr>  
  <tr>
    <td><code>@(bar|baz)</code></td>
    <td><code>bar</code>,&nbsp;<code>baz</code></td>
    <td>One of the given subpatterns exactly one time</td>
  </tr>   
  <tr>
    <td><code>?(foo)</code><br><code>?(bar|baz)</code></td>
    <td>empty&nbsp;string,&nbsp;<code>foo</code><br>empty&nbsp;string,&nbsp;<code>bar</code>,&nbsp;<code>baz</code></td>
    <td>One of the given subpatterns zero or one time</td>
  </tr>    
  <tr>
    <td><code>*(foo)</code><br><code>*(bar|baz)</code></td>
    <td>empty&nbsp;string,&nbsp;<code>foo</code>,&nbsp;<code>foofoofoo</code><br>empty&nbsp;string,&nbsp;<code>bar</code>,&nbsp;<code>bazbaz</code>,&nbsp;<code>barbaz</code></td>
    <td>One of the given subpatterns zero or more times</td>
  </tr>    
  <tr>
    <td><code>+(foo)</code><br><code>+(bar|baz)</code></td>
    <td><code>foo</code>,&nbsp;<code>foofoofoo</code><br><code>bar</code>,&nbsp;<code>bazbaz</code>,&nbsp;<code>barbaz</code></td>
    <td>One of the given subpatterns one or more times</td>
  </tr>    
  <tr>
    <td><code>!(foo)</code><br><code>!(bar|baz)</code></td>
    <td>any&nbsp;string&nbsp;except&nbsp;<code>foo</code><br>any&nbsp;string&nbsp;except&nbsp;<code>bar</code>,&nbsp;<code>baz</code></td>
    <td>Anything except for the given subpatterns</td>
  </tr>
</table>

### Braces

Brace expansion is a feature of Bash that generates a list of strings from a single source pattern. In the pattern, parts that should differ between the strings are put in curly braces, and the rest is left intact. For example, `src/{foo,bar}/baz` would be expanded to two strings, `src/foo/baz` and `src/bar/baz`.

Pattern     | Matches                           | Description
----------- | --------------------------------- | -----------
`{bar,baz}` | `bar`,&nbsp;`baz`                 | Matches one of the subpatterns
`{1..5}`    | 1,&nbsp;2,&nbsp;3,&nbsp;4,&nbsp;5 | Matches any number from the range

This feature is similar to extglobs, but they work differently. Extglobs are converted to RegExp groups (`@(bar|baz)` → `(bar|baz)`) while braces expand a single pattern into an array of patterns, so `outmatch('foo/{bar,baz}')` becomes `outmatch(['foo/bar', 'foo/baz'])`. 

Braces are processed _before anything else_, so, unlike extglobs, they work even with subpatterns that contain separators:

```js
const isMatch = outmatch('src/{foo,bar/baz}')

isMatch('src/foo') //=> true
isMatch('src/bar/baz') //=> true
isMatch('src/bar') //=> false
```

Braces can be nested:

```js
const isMatch = outmatch('{one,{two,three}}')

isMatch('one') //=> true
isMatch('two') //=> true
isMatch('three') //=> true
```

### Escaping

Preceding a special character with a backslash `\` escapes the character making it be treated literally:

```js
const isMatch = outmatch('foo\?*')

isMatch('foo?') //=> true
isMatch('foob') //=> false
```

### Negation

Patterns can be negated by putting an exclamation mark `!` at the beginning. A negated pattern matches any string that doesn't match the part after the `!`:

```js
const isMatch = outmatch('!src/*')

isMatch('foo') //=> true
isMatch('src/foo/bar') //=> true
isMatch('src/foo') //=> false
```

When put in an array among positive patterns, negated patterns effectively work as ignores:

```js
const isMatch = outmatch(['src/*', '!src/bar'])

isMatch('src/foo') //=> true
isMatch('src/bar') //=> false
```

Exclamation marks can be repeated multiple times. Each mark will invert the pattern, so `!!foo/bar` is the same as `foo/bar` and `!!!baz/qux` is the same as `!baz/qux`.

## API

### outmatch(patterns, options?): isMatch

Takes a single pattern string or an array of patterns and compiles them into a regular expression. Returns an isMatch function that takes a sample string as its only argument and returns true if the string matches the patterns.

### isMatch(sample): boolean

Tests if a sample string matches the patterns that were used to compile the regular expression and create this function.

### isMatch.regExp

The compiled regular expression.

### isMatch.pattern

The original pattern or array of patterns that was used to compile the regular expression and create the isMatch function.

### isMatch.options

The options object that was used to compile the regular expression and create the isMatch function.

## Comparison

Coming soon.

## License

[ISC](LICENSE)

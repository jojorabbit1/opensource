# parse-commit-message [![npm version][npmv-img]][npmv-url] [![License][license-img]][license-url] [![Libera Manifesto][libera-manifesto-img]][libera-manifesto-url]

> Extensible parser for git commit messages following Conventional Commits
> Specification

Please consider following this project's author,
[Charlike Mike Reagent](https://github.com/tunnckoCore), and :star: the project
to show your :heart: and support.

<div id="readme"></div>

[![Code style][codestyle-img]][codestyle-url]
[![CircleCI linux build][linuxbuild-img]][linuxbuild-url]
[![CodeCov coverage status][codecoverage-img]][codecoverage-url]
[![Renovate App Status][renovateapp-img]][renovateapp-url]
[![Make A Pull Request][prs-welcome-img]][prs-welcome-url]
[![Time Since Last Commit][last-commit-img]][last-commit-url]

<!-- [![Semantically Released][standard-release-img]][standard-release-url] -->

If you have any _how-to_ kind of questions, please read the [Contributing
Guide][contributing-url] and [Code of Conduct][code_of_conduct-url] documents.
For bugs reports and feature requests, [please create an issue][open-issue-url]
or ping [@tunnckoCore](https://twitter.com/tunnckoCore) at Twitter.

[![Conventional Commits][ccommits-img]][ccommits-url]
[![Minimum Required Nodejs][nodejs-img]][npmv-url]
[![NPM Downloads Monthly][downloads-monthly-img]][npmv-url]
[![NPM Downloads Total][downloads-total-img]][npmv-url]
[![Share Love Tweet][twitter-share-img]][twitter-share-url]
[![Twitter][twitter-img]][twitter-url]

Project is [semantically](https://semver.org) versioned & automatically released
from [GitHub Actions](https://github.com/features/actions) with
[Lerna](https://github.com/lerna/lerna).

[![Become a Patron][patreon-img]][patreon-url]
[![Buy me a Kofi][kofi-img]][kofi-url]
[![PayPal Donation][paypal-img]][paypal-url]
[![Bitcoin Coinbase][bitcoin-img]][bitcoin-url]
[![Keybase PGP][keybase-img]][keybase-url]

| Topic                                                            |                                           Contact |
| :--------------------------------------------------------------- | ------------------------------------------------: |
| Any legal or licensing questions, like private or commerical use |           ![tunnckocore_legal][tunnckocore_legal] |
| For any critical problems and security reports                   |     ![tunnckocore_security][tunnckocore_security] |
| Consulting, professional support, personal or team training      | ![tunnckocore_consulting][tunnckocore_consulting] |
| For any questions about Open Source, partnerships and sponsoring | ![tunnckocore_opensource][tunnckocore_opensource] |

<!-- Logo when needed:

<p align="center">
  <a href="https://github.com/tunnckoCore/opensource">
    <img src="./media/logo.png" width="85%">
  </a>
</p>

-->

## Table of Contents

- [Install](#install)
- [API](#api)
  - [isBreakingChangePlugin](#isbreakingchangeplugin)
  - [mentionsPlugin](#mentionsplugin)
  - [.parseHeader](#parseheader)
  - [.stringifyHeader](#stringifyheader)
  - [.validateHeader](#validateheader)
  - [.checkHeader](#checkheader)
  - [.applyPlugins](#applyplugins)
  - [.plugins](#plugins)
  - [.mappers](#mappers)
  - [.parseCommit](#parsecommit)
  - [.stringifyCommit](#stringifycommit)
  - [.validateCommit](#validatecommit)
  - [.checkCommit](#checkcommit)
  - [.parse](#parse)
  - [.stringify](#stringify)
  - [.validate](#validate)
  - [.check](#check)
  - [incrementPlugin](#incrementplugin)
- [Contributing](#contributing)
  - [Guides and Community](#guides-and-community)
  - [Support the project](#support-the-project)
- [Contributors](#contributors)
- [License](#license)

_(TOC generated by [verb](https://github.com/verbose/verb) using
[markdown-toc](https://github.com/jonschlinkert/markdown-toc))_

## Install

This project requires [**Node.js**](https://nodejs.org) **>=10.13.0** _(see
[Support & Release Policy](https://github.com/tunnckoCoreLabs/support-release-policy))_.
Install it using [**yarn**](https://yarnpkg.com) or
[**npm**](https://npmjs.com).<br> _We highly recommend to use Yarn when you
think to contribute to this project._

```bash
$ yarn add parse-commit-message
```

## API

<!-- docks-start -->

_Generated using [jest-runner-docs](https://ghub.now.sh/jest-runner-docs)._

### [isBreakingChangePlugin](./src/plugins/is-breaking-change.js#L30)

A plugin that adds `isBreakingChange` and `isBreaking` (_deprecated_) properties
to the `commit`. It is already included in the `plugins` named export, and in
`mappers` named export. Be aware that there's a difference between the utility
`isBreakingChange` which has named export (as everything from `src/utils`) and
this plugin function.

**Note: This plugin was included in v4 release version, previously was part of
the `increment` plugin.**

<span id="isbreakingchangeplugin-signature"></span>

#### Signature

```ts
function(commit, options)
```

<span id="isbreakingchangeplugin-params"></span>

#### Params

- `commit` **{Commit}** - a standard `Commit` object
- `options` **{object}** - options to control the header regex and case
  sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or
  instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive,
  defaults to `false`
- `returns` **{Commit}** - plus `{ isBreakingChange: boolean }`

_See the [.plugins](#plugins) and [.mappers](#mappers) examples._

<span id="isbreakingchangeplugin-examples"></span>

#### Examples

```js
import { mappers, plugins } from 'parse-commit-message';

console.log(mappers.isBreakingChange); // => [Function: isBreakingChangePlugin]
console.log(plugins[2]); // => [Function: isBreakingChangePlugin]
```

_Generated using [jest-runner-docs](https://ghub.now.sh/jest-runner-docs)._

### [mentionsPlugin](./src/plugins/mentions.js#L27)

A plugin that adds `mentions` array property to the `commit`. It is already
included in the `plugins` named export, and in `mappers` named export. Basically
each entry in that array is an object, directly returned from the
[collect-mentions][].

<span id="mentionsplugin-signature"></span>

#### Signature

```ts
function(commit, options)
```

<span id="mentionsplugin-params"></span>

#### Params

- `commit` **{Commit}** - a standard `Commit` object
- `options` **{object}** - options to control the header regex and case
  sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or
  instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive,
  defaults to `false`
- `returns` **{Commit}** - plus `{ mentions: Array<Mention> }`

_See the [.plugins](#plugins) and [.mappers](#mappers) examples._

<span id="mentionsplugin-examples"></span>

#### Examples

```js
import { mappers, plugins } from 'parse-commit-message';

console.log(mappers.mentions); // => [Function: mentionsPlugin]
console.log(plugins[0]); // => [Function: mentionsPlugin]
```

_Generated using [jest-runner-docs](https://ghub.now.sh/jest-runner-docs)._

### [.parseHeader](./src/header.js#L31)

Parses given `header` string into an header object. Basically the same as
[.parse](#parse), except that it only can accept single string and returns a
`Header` object.

<span id="parseheader-signature"></span>

#### Signature

```ts
function(header, options)
```

<span id="parseheader-params"></span>

#### Params

- `header` **{string}** - a header stirng like `'fix(foo): bar baz'`
- `options` **{object}** - options to control the header regex and case
  sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or
  instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive,
  defaults to `false`
- `returns` **{Header}** - a `Header` object like `{ type, scope?, subject }`

_The `parse*` methods are not doing any checking and validation, so you may want
to pass the result to `validateHeader` or `checkHeader`, or to `validateHeader`
with `ret` option set to `true`._

<span id="parseheader-examples"></span>

#### Examples

```js
import { parseHeader } from 'parse-commit-message';

const longCommitMsg = `fix: bar qux

Awesome body!`;

const headerObj = parseCommit(longCommitMsg);
console.log(headerObj);
// => { type: 'fix', scope: null, subject: 'bar qux' }
```

### [.stringifyHeader](./src/header.js#L59)

Receives a `header` object, validates it using `validateHeader`, builds a
"header" string and returns it. Method throws if problems found. Basically the
same as [.stringify](#stringify), except that it only can accept single `Header`
object.

<span id="stringifyheader-signature"></span>

#### Signature

```ts
function(header, options)
```

<span id="stringifyheader-params"></span>

#### Params

- `header` **{Header}** - a `Header` object like `{ type, scope?, subject }`
- `options` **{object}** - options to control the header regex and case
  sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or
  instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive,
  defaults to `false`
- `returns` **{string}** - a header stirng like `'fix(foo): bar baz'`

<span id="stringifyheader-examples"></span>

#### Examples

```js
import { stringifyHeader } from 'parse-commit-message';

const headerStr = stringifyCommit({ type: 'foo', subject: 'bar qux' });
console.log(headerStr); // => 'foo: bar qux'
```

### [.validateHeader](./src/header.js#L115)

Validates given `header` object and returns `boolean`. You may want to pass
`ret` to return an object instead of throwing. Basically the same as
[.validate](#validate), except that it only can accept single `Header` object.

<span id="validateheader-signature"></span>

#### Signature

```ts
function(header, options)
```

<span id="validateheader-params"></span>

#### Params

- `header` **{Header}** - a `Header` object like `{ type, scope?, subject }`
- `options` **{object}** - options to control the header regex and case
  sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or
  instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive,
  defaults to `false`
- `returns` **{CommitResult}** - an object like
  `{ value: Array<Commit>, error: Error }`

<span id="validateheader-examples"></span>

#### Examples

```js
import { validateHeader } from 'parse-commit-message';

const header = { type: 'foo', subject: 'bar qux' };

const headerIsValid = validateHeader(header);
console.log(headerIsValid); // => true

const { value } = validateHeader(header, true);
console.log(value);
// => {
//   header: { type: 'foo', scope: null, subject: 'bar qux' },
//   body: 'okey dude',
//   footer: null,
// }

const { error } = validateHeader(
  {
    type: 'bar',
  },
  true,
);

console.log(error);
// => TypeError: header.subject should be non empty string
```

### [.checkHeader](./src/header.js#L156)

Receives a `Header` and checks if it is valid. Basically the same as
[.check](#check), except that it only can accept single `Header` object.

<span id="checkheader-signature"></span>

#### Signature

```ts
function(header, options)
```

<span id="checkheader-params"></span>

#### Params

- `header` **{Header}** - a `Header` object like `{ type, scope?, subject }`
- `options` **{object}** - options to control the header regex and case
  sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or
  instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive,
  defaults to `false`
- `returns` **{Header}** - returns the same as given if no problems, otherwise
  it will throw.

<span id="checkheader-examples"></span>

#### Examples

```js
import { checkHeader } from 'parse-commit-message';

try {
  checkHeader({ type: 'fix' });
} catch (err) {
  console.log(err);
  // => TypeError: header.subject should be non empty string
}

// throws because can accept only Header objects
checkHeader('foo bar baz');
checkHeader(123);
checkHeader([]);
checkHeader([{ type: 'foo', subject: 'bar' }]);
```

_Generated using [jest-runner-docs](https://ghub.now.sh/jest-runner-docs)._

### [.applyPlugins](./src/index.js#L102)

Apply a set of `plugins` over all of the given `commits`. A plugin is a simple
function passed with `Commit` object, which may be returned to modify and set
additional properties to the `Commit` object.

<span id="applyplugins-signature"></span>

#### Signature

```ts
function(plugins, commits, options)
```

<span id="applyplugins-params"></span>

#### Params

- `plugins` **{Plugins}** - a simple function like `(commit) => {}`
- `commits` **{PossibleCommit}** - a PossibleCommit or an array of strings; a
  value which should already be gone through `parse`
- `options` **{object}** - options to control the header regex and case
  sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or
  instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive,
  defaults to `false`
- `returns` **{Array&lt;Commit&gt;}** - plus the modified or added properties
  from each function in `plugins`

_The `commits` should be coming from `parse`, `validate` (with `ret` option) or
the `check` methods. It does not do checking and validation._

<span id="applyplugins-examples"></span>

#### Examples

```js
import dedent from 'dedent';
import { applyPlugins, plugins, parse, check } from 'parse-commit-message';

const commits = [
  'fix: bar qux',
  dedent`feat(foo): yea yea

  Awesome body here with @some mentions
  resolves #123

  BREAKING CHANGE: ouch!`,
  'chore(ci): updates for ci config',
  {
    header: { type: 'fix', subject: 'Barry White' },
    body: 'okey dude',
    foo: 'possible',
  },
];

// Parses, normalizes, validates
// and applies plugins
const results = applyPlugins(plugins, check(parse(commits)));

console.log(results);
// => [ { body: null,
//   footer: null,
//   header: { scope: null, type: 'fix', subject: 'bar qux' },
//   mentions: [],
//   increment: 'patch',
//   isBreaking: false },
// { body: 'Awesome body here with @some mentions\nresolves #123',
//   footer: 'BREAKING CHANGE: ouch!',
//   header: { scope: 'foo', type: 'feat', subject: 'yea yea' },
//   mentions: [ [Object] ],
//   increment: 'major',
//   isBreaking: true },
// { body: null,
//   footer: null,
//   header:
//    { scope: 'ci', type: 'chore', subject: 'updates for ci config' },
//   mentions: [],
//   increment: false,
//   isBreaking: false },
// { body: 'okey dude',
//   footer: null,
//   header: { scope: null, type: 'fix', subject: 'Barry White' },
//   foo: 'possible',
//   mentions: [],
//   increment: 'patch',
//   isBreaking: false } ]
```

### [.plugins](./src/index.js#L186)

An array which includes `mentions`, `isBreakingChange` and `increment` built-in
plugins. The `mentions` is an array of objects - basically what's returned from
the [collect-mentions][] package.

<span id="plugins-examples"></span>

#### Examples

```js
import { plugins, applyPlugins, parse } from 'parse-commit-message';

console.log(plugins); // =>  [mentions, increment]
console.log(plugins[0]); // => [Function mentions]
console.log(plugins[0]); // => [Function increment]

const cmts = parse([
  'fix: foo @bar @qux haha',
  'feat(cli): awesome @tunnckoCore feature\n\nSuper duper baz!'
  'fix: ooh\n\nBREAKING CHANGE: some awful api change'
]);

const commits = applyPlugins(plugins, cmts);
console.log(commits);
// => [
//   {
//     header: { type: 'fix', scope: '', subject: 'foo bar baz' },
//     body: '',
//     footer: '',
//     increment: 'patch',
//     isBreaking: false,
//     mentions: [
//       { handle: '@bar', mention: 'bar', index: 8 },
//       { handle: '@qux', mention: 'qux', index: 13 },
//     ]
//   },
//   {
//     header: { type: 'feat', scope: 'cli', subject: 'awesome feature' },
//     body: 'Super duper baz!',
//     footer: '',
//     increment: 'minor',
//     isBreaking: false,
//     mentions: [
//       { handle: '@tunnckoCore', mention: 'tunnckoCore', index: 18 },
//     ]
//   },
//   {
//     header: { type: 'fix', scope: '', subject: 'ooh' },
//     body: 'BREAKING CHANGE: some awful api change',
//     footer: '',
//     increment: 'major',
//     isBreaking: true,
//     mentions: [],
//   },
// ]
```

### [.mappers](./src/index.js#L219)

An object (named set) which includes `mentions` and `increment` built-in
plugins.

<span id="mappers-examples"></span>

#### Examples

```js
import { mappers, applyPlugins, parse } from 'parse-commit-message';

console.log(mappers); // => { mentions, increment }
console.log(mappers.mentions); // => [Function mentions]
console.log(mappers.increment); // => [Function increment]

const flat = true;
const parsed = parse('fix: bar', flat);
console.log(parsed);
// => {
//   header: { type: 'feat', scope: 'cli', subject: 'awesome feature' },
//   body: 'Super duper baz!',
//   footer: '',
// }

const commit = applyPlugins([mappers.increment], parsed);
console.log(commit);
// => [{
//   header: { type: 'feat', scope: 'cli', subject: 'awesome feature' },
//   body: 'Super duper baz!',
//   footer: '',
//   increment: 'patch',
// }]
```

_Generated using [jest-runner-docs](https://ghub.now.sh/jest-runner-docs)._

### [.parseCommit](./src/commit.js#L33)

Receives a full commit message `string` and parses it into an `Commit` object
and returns it. Basically the same as [.parse](#parse), except that it only can
accept single string.

<span id="parsecommit-signature"></span>

#### Signature

```ts
function(commit, options)
```

<span id="parsecommit-params"></span>

#### Params

- `commit` **{string}** - a message like
  `'fix(foo): bar baz\n\nSome awesome body!'`
- `options` **{object}** - options to control the header regex and case
  sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or
  instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive,
  defaults to `false`
- `returns` **{Commit}** - a standard object like
  `{ header: Header, body?, footer? }`

_The `parse*` methods are not doing any checking and validation, so you may want
to pass the result to `validateCommit` or `checkCommit`, or to `validateCommit`
with `ret` option set to `true`._

<span id="parsecommit-examples"></span>

#### Examples

```js
import { parseCommit } from 'parse-commit-message';

const commitObj = parseCommit('foo: bar qux\n\nokey dude');
console.log(commitObj);
// => {
//   header: { type: 'foo', scope: null, subject: 'bar qux' },
//   body: 'okey dude',
//   footer: null,
// }
```

### [.stringifyCommit](./src/commit.js#L67)

Receives a `Commit` object, validates it using `validateCommit`, builds a
"commit" string and returns it. Method throws if problems found. Basically the
same as [.stringify](#stringify), except that it only can accept single `Commit`
object.

<span id="stringifycommit-signature"></span>

#### Signature

```ts
function(commit, options)
```

<span id="stringifycommit-params"></span>

#### Params

- `commit` **{Commit}** - a `Commit` object like
  `{ header: Header, body?, footer? }`
- `options` **{object}** - options to control the header regex and case
  sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or
  instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive,
  defaults to `false`
- `returns` **{string}** - a commit nessage stirng like `'fix(foo): bar baz'`

<span id="stringifycommit-examples"></span>

#### Examples

```js
import { stringifyCommit } from 'parse-commit-message';

const commitStr = stringifyCommit({
  header: { type: 'foo', subject: 'bar qux' },
  body: 'okey dude',
});
console.log(commitStr); // => 'foo: bar qux\n\nokey dude'
```

### [.validateCommit](./src/commit.js#L117)

Validates given `Commit` object and returns `CommitResult`. Basically the same
as [.validate](#validate), except that it only can accept single `Commit`
object.

<span id="validatecommit-signature"></span>

#### Signature

```ts
function(commit, options)
```

<span id="validatecommit-params"></span>

#### Params

- `commit` **{Commit}** - a `Commit` like `{ header: Header, body?, footer? }`
- `options` **{object}** - options to control the header regex and case
  sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or
  instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive,
  defaults to `false`
- `returns` **{CommitResult}** - an object like
  `{ value: Array<Commit>, error: Error }`

<span id="validatecommit-examples"></span>

#### Examples

```js
import { validateCommit } from 'parse-commit-message';

const commit = {
  header: { type: 'foo', subject: 'bar qux' },
  body: 'okey dude',
};

const commitIsValid = validateCommit(commit);
console.log(commitIsValid); // => true

const { value } = validateCommit(commit, true);
console.log(value);
// => {
//   header: { type: 'foo', scope: null, subject: 'bar qux' },
//   body: 'okey dude',
//   footer: null,
// }
```

### [.checkCommit](./src/commit.js#L157)

Receives a `Commit` and checks if it is valid. Method throws if problems found.
Basically the same as [.check](#check), except that it only can accept single
`Commit` object.

<span id="checkcommit-signature"></span>

#### Signature

```ts
function(commit, options)
```

<span id="checkcommit-params"></span>

#### Params

- `commit` **{Commit}** - a `Commit` like `{ header: Header, body?, footer? }`
- `options` **{object}** - options to control the header regex and case
  sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or
  instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive,
  defaults to `false`
- `returns` **{Commit}** - returns the same as given if no problems, otherwise
  it will throw.

<span id="checkcommit-examples"></span>

#### Examples

```js
import { checkCommit } from 'parse-commit-message';

try {
  checkCommit({ header: { type: 'fix' } });
} catch (err) {
  console.log(err);
  // => TypeError: header.subject should be non empty string
}

// throws because can accept only Commit objects
checkCommit('foo bar baz');
checkCommit(123);
checkCommit([{ header: { type: 'foo', subject: 'bar' } }]);
```

_Generated using [jest-runner-docs](https://ghub.now.sh/jest-runner-docs)._

### [.parse](./src/main.js#L51)

Receives and parses a single or multiple commit message(s) in form of string,
object, array of strings, array of objects or mixed.

<span id="parse-signature"></span>

#### Signature

```ts
function(commits, options)
```

<span id="parse-params"></span>

#### Params

- `commits` **{PossibleCommit}** - a value to be parsed into an object like
  `Commit` type
- `options` **{object}** - options to control the header regex and case
  sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or
  instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive,
  defaults to `false`
- `returns` **{Array&lt;Commit&gt;}** - if array of commit objects

<span id="parse-examples"></span>

#### Examples

```js
import { parse } from 'parse-commit-message';

const commits = ['fix(ci): tweaks for @circleci config', 'chore: bar qux'];
const result = parse(commits);
console.log(result);
// => [{
//   header: { type: 'fix', scope: 'ci', subject: 'tweaks for @circleci config' },
//   body: null,
//   footer: null,
// }, {
//   header: { type: 'chore', scope: null, subject: 'bar qux' },
//   body: null,
//   footer: null,
// }]

const commitMessage = `feat: awesome yeah

Awesome body!
resolves #123

Signed-off-by: And Footer <abc@exam.pl>`;

const res = parse(commitMessage);

console.log(res);
// => {
//   header: { type: 'feat', scope: null, subject: 'awesome yeah' },
//   body: 'Awesome body!\nresolves #123',
//   footer: 'Signed-off-by: And Footer <abc@exam.pl>',
// }
```

### [.stringify](./src/main.js#L101)

Receives a `Commit` object, validates it using `validate`, builds a "commit"
message string and returns it.

<span id="stringify-signature"></span>

#### Signature

```ts
function(commits, options)
```

<span id="stringify-params"></span>

#### Params

- `commits` **{PossibleCommit}** - a `Commit` object, or anything that can be
  passed to `check`
- `options` **{object}** - options to control the header regex and case
  sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or
  instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive,
  defaults to `false`
- `returns` **{Array&lt;string&gt;}** - an array of commit strings like
  `'fix(foo): bar baz'`

This method does checking and validation too, so if you pass a string, it will
be parsed and validated, and after that turned again to string.

<span id="stringify-examples"></span>

#### Examples

```js
import { parse, stringify } from 'parse-commit-message';

const commitMessage = `feat: awesome yeah

Awesome body!
resolves #123

Signed-off-by: And Footer <abc@exam.pl>`;

const flat = true;
const res = parse(commitMessage, flat);

const str = stringify(res, flat);
console.log(str);
console.log(str === commitMessage);
```

### [.validate](./src/main.js#L181)

Validates a single or multiple commit message(s) in form of string, object,
array of strings, array of objects or mixed.

<span id="validate-signature"></span>

#### Signature

```ts
function(commits, options)
```

<span id="validate-params"></span>

#### Params

- `commits` **{PossibleCommit}** - a value to be parsed & validated into an
  object like `Commit` type
- `options` **{object}** - options to control the header regex and case
  sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or
  instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive,
  defaults to `false`
- `returns` **{CommitResult}** - an object like
  `{ value: Array<Commit>, error: Error }`

<span id="validate-examples"></span>

#### Examples

```js
import { validate } from 'parse-commit-message';

console.log(validate('foo bar qux')); // false
console.log(validate('foo: bar qux')); // true
console.log(validate('fix(ci): bar qux')); // true

console.log(validate(['a bc cqux', 'foo bar qux'])); // false

console.log(validate({ qux: 1 })); // false
console.log(validate({ header: { type: 'fix' } })); // false
console.log(validate({ header: { type: 'fix', subject: 'ok' } })); // true

const commitObject = {
  header: { type: 'test', subject: 'updating tests' },
  foo: 'bar',
  isBreaking: false,
  body: 'oh ah',
};
console.log(validate(commitObject)); // true

const result = validate('foo bar qux');
console.log(result.error);
// => Error: expect \`commit\` to follow:
// <type>[optional scope]: <description>
//
// [optional body]
//
// [optional footer]

const res = validate('fix(ci): okey barry');
console.log(result.value);
// => [{
//   header: { type: 'fix', scope: 'ci', subject: 'okey barry' },
//   body: null,
//   footer: null,
// }]

const commit = { header: { type: 'fix' } };
const { error } = validate(commit);
console.log(error);
// => TypeError: header.subject should be non empty string

const commit = { header: { type: 'fix', scope: 123, subject: 'okk' } };
const { error } = validate(commit);
console.log(error);
// => TypeError: header.scope should be non empty string when given
```

### [.check](./src/main.js#L225)

Receives a single or multiple commit message(s) in form of string, object, array
of strings, array of objects or mixed. Throws if find some error. Think of it as
"assert", it's basically that.

<span id="check-signature"></span>

#### Signature

```ts
function(commits, options)
```

<span id="check-params"></span>

#### Params

- `commits` **{PossibleCommit}** - a value to be parsed & validated into an
  object like `Commit` type
- `options` **{object}** - options to control the header regex and case
  sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or
  instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive,
  defaults to `false`
- `returns` **{Array&lt;Commit&gt;}** - returns the same as given if no
  problems, otherwise it will throw;

<span id="check-examples"></span>

#### Examples

```js
import { check } from 'parse-commit-message';

try {
  check({ header: { type: 'fix' } });
} catch (err) {
  console.log(err);
  // => TypeError: header.subject should be non empty string
}

// Can also validate/check a strings, array of strings,
// or even mixed - array of strings and objects
try {
  check('fix(): invalid scope, it cannot be empty');
} catch (err) {
  console.log(err);
  // => TypeError: header.scope should be non empty string when given
}
```

_Generated using [jest-runner-docs](https://ghub.now.sh/jest-runner-docs)._

### [incrementPlugin](./src/plugins/increment.js#L26)

A plugin that adds `increment` property to the `commit`. It is already included
in the `plugins` named export, and in `mappers` named export.

**Note: Since v4 this plugin doesn't add `isBreaking` property, use the
`isBreaking` plugin instead.**

<span id="incrementplugin-signature"></span>

#### Signature

```ts
function(commit, options)
```

<span id="incrementplugin-params"></span>

#### Params

- `commit` **{Commit}** - a standard `Commit` object
- `options` **{object}** - options to control the header regex and case
  sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or
  instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive,
  defaults to `false`
- `returns` **{Commit}** - plus `{ increment: string }`

_See the [.plugins](#plugins) and [.mappers](#mappers) examples._

<span id="incrementplugin-examples"></span>

#### Examples

```js
import { mappers, plugins } from 'parse-commit-message';

console.log(mappers.increment); // => [Function: incrementPlugin]
console.log(plugins[1]); // => [Function: incrementPlugin]
```

<!-- docks-end -->

**[back to top](#readme)**

## Contributing

### Guides and Community

Please read the [Contributing Guide][contributing-url] and [Code of
Conduct][code_of_conduct-url] documents for advices.

For bug reports and feature requests, please join our [community][community-url]
forum and open a thread there with prefixing the title of the thread with the
name of the project if there's no separate channel for it.

Consider reading the
[Support and Release Policy](https://github.com/tunnckoCoreLabs/support-release-policy)
guide if you are interested in what are the supported Node.js versions and how
we proceed. In short, we support latest two even-numbered Node.js release lines.

### Support the project

[Become a Partner or Sponsor?][kofi-url] :dollar: Check the **OpenSource**
Commision (tier). :tada: You can get your company logo, link & name on this
file. It's also rendered on package's page in [npmjs.com][npmv-url] and
[yarnpkg.com](https://yarnpkg.com/en/package/parse-commit-message) sites too!
:rocket:

Not financial support? Okey!
[Pull requests](https://github.com/tunnckoCoreLabs/contributing#opening-a-pull-request),
stars and all kind of
[contributions](https://opensource.guide/how-to-contribute/#what-it-means-to-contribute)
are always welcome. :sparkles:

## Contributors

This project follows the
[all-contributors](https://github.com/all-contributors/all-contributors)
specification. Contributions of any kind are welcome!

Thanks goes to these wonderful people
([emoji key](https://allcontributors.org/docs/en/emoji-key)), consider showing
your [support](#support-the-project) to them:

<!-- ALL-CONTRIBUTORS-LIST:START -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://tunnckoCore.com"><img src="https://avatars3.githubusercontent.com/u/5038030?v=4" width="100px;" alt=""/><br /><sub><b>Charlike Mike Reagent</b></sub></a><br /><a href="#infra-tunnckoCore" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a> <a href="https://github.com/node-formidable/node-formidable/commits?author=tunnckoCore" title="Code">💻</a> <a href="https://github.com/node-formidable/node-formidable/commits?author=tunnckoCore" title="Documentation">📖</a> <a href="#ideas-tunnckoCore" title="Ideas, Planning, & Feedback">🤔</a> <a href="#maintenance-tunnckoCore" title="Maintenance">🚧</a> <a href="https://github.com/node-formidable/node-formidable/commits?author=tunnckoCore" title="Tests">⚠️</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

**[back to top](#readme)**

## License

Copyright (c) 2018-present, [Charlike Mike Reagent](https://tunnckocore.com)
`<opensource@tunnckocore.com>` & [contributors](#wonderful-contributors).<br>
Released under the [MPL-2.0 License][license-url].

<!-- badges -->

<!-- prettier-ignore-start -->

[contributing-url]: https://github.com/tunnckoCore/opensource/blob/master/CONTRIBUTING.md
[code_of_conduct-url]: https://github.com/tunnckoCore/opensource/blob/master/CODE_OF_CONDUCT.md

<!-- Heading badges -->

[npmv-url]: https://www.npmjs.com/package/parse-commit-message
[npmv-img]: https://badgen.net/npm/v/parse-commit-message?icon=npm&cache=300

[license-url]: https://github.com/tunnckoCore/opensource/blob/master/packages/parse-commit-message/LICENSE
[license-img]: https://badgen.net/npm/license/parse-commit-message?cache=300

[libera-manifesto-url]: https://liberamanifesto.com
[libera-manifesto-img]: https://badgen.net/badge/libera/manifesto/grey

<!-- Front line badges -->

[codecoverage-img]: https://badgen.net/badge/coverage/65.61%25/orange?icon=codecov&cache=300

[codecoverage-url]: https://codecov.io/gh/tunnckoCore/opensource

[codestyle-url]: https://github.com/airbnb/javascript
[codestyle-img]: https://badgen.net/badge/code%20style/airbnb/ff5a5f?icon=airbnb&cache=300

[linuxbuild-url]: https://github.com/tunnckocore/opensource/actions
[linuxbuild-img]: https://badgen.net/github/checks/tunnckoCore/opensource/master?cache=300&label=build&icon=github

[ccommits-url]: https://conventionalcommits.org/
[ccommits-img]: https://badgen.net/badge/conventional%20commits/v1.0.0/green?cache=300

[standard-release-url]: https://github.com/standard-release/standard-release
[standard-release-img]: https://badgen.net/badge/semantically/released/05c5ff?cache=300

[community-img]: https://badgen.net/badge/join/community/7b16ff?cache=300
[community-url]: https://github.com/tunnckocorehq/community

[last-commit-img]: https://badgen.net/github/last-commit/tunnckoCore/opensource/master?cache=300
[last-commit-url]: https://github.com/tunnckoCore/opensource/commits/master

[nodejs-img]: https://badgen.net/badge/node/>=10.13.0/green?cache=300

[downloads-weekly-img]: https://badgen.net/npm/dw/parse-commit-message?icon=npm&cache=300
[downloads-monthly-img]: https://badgen.net/npm/dm/parse-commit-message?icon=npm&cache=300
[downloads-total-img]: https://badgen.net/npm/dt/parse-commit-message?icon=npm&cache=300

[renovateapp-url]: https://renovatebot.com
[renovateapp-img]: https://badgen.net/badge/renovate/enabled/green?cache=300

[prs-welcome-img]: https://badgen.net/badge/PRs/welcome/green?cache=300
[prs-welcome-url]: http://makeapullrequest.com

<!-- TODO: update icon -->

[paypal-url]: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=HYJJEZNSGAPGC&source=url
[paypal-img]: https://badgen.net/badge/PayPal/donate/003087?cache=300&icon=https://simpleicons.now.sh/paypal/fff

<!-- TODO: update icon -->

[kofi-url]: https://ko-fi.com/tunnckoCore
[kofi-img]: https://badgen.net/badge/Buy%20me/a%20coffee/29abe0c2?cache=300&icon=https://rawcdn.githack.com/tunnckoCore/badgen-icons/f8264c6414e0bec449dd86f2241d50a9b89a1203/icons/kofi.svg

<!-- TODO: update icon -->

[bitcoin-url]: https://www.blockchain.com/btc/payment_request?address=3QNHKun1K1SUui1b4Z3KEGPPsWC1TgtnqA&message=Open+Source+Software&amount_local=10&currency=USD
[bitcoin-img]: https://badgen.net/badge/Bitcoin%20tip/3QNHKun...b4Z3KEGPPsWC1TgtnqA/yellow?cache=300&icon=https://simpleicons.now.sh/bitcoin/fff
[keybase-url]: https://keybase.io/tunnckoCore
[keybase-img]: https://badgen.net/keybase/pgp/tunnckoCore?cache=300
[twitter-url]: https://twitter.com/tunnckoCore
[twitter-img]: https://badgen.net/twitter/follow/tunnckoCore?icon=twitter&color=1da1f2&cache=300
[patreon-url]: https://www.patreon.com/bePatron?u=5579781
[patreon-img]: https://badgen.net/badge/Become/a%20patron/F96854?icon=patreon

<!-- [patreon-img]: https://badgen.net/badge/Patreon/tunnckoCore/F96854?icon=patreon -->

[patreon-sponsor-img]: https://badgen.net/badge/become/a%20sponsor/F96854?icon=patreon
[twitter-share-url]: https://twitter.com/intent/tweet?text=https://github.com/tunnckoCore/opensource/tree/master&via=tunnckoCore
[twitter-share-img]: https://badgen.net/badge/twitter/share/1da1f2?icon=twitter
[open-issue-url]: https://github.com/tunnckoCore/opensource/issues/new
[tunnckocore_legal]: https://badgen.net/https/liam-badge-daknys6gadky.runkit.sh/com/legal/tunnckocore?label&color=A56016&icon=https://svgshare.com/i/Dt6.svg
[tunnckocore_consulting]: https://badgen.net/https/liam-badge-daknys6gadky.runkit.sh/com/consulting/tunnckocore?label&color=07ba96&icon=https://svgshare.com/i/Dt6.svg
[tunnckocore_security]: https://badgen.net/https/liam-badge-daknys6gadky.runkit.sh/com/security/tunnckocore?label&color=ed1848&icon=https://svgshare.com/i/Dt6.svg
[tunnckocore_opensource]: https://badgen.net/https/liam-badge-daknys6gadky.runkit.sh/com/opensource/tunnckocore?label&color=ff7a2f&icon=https://svgshare.com/i/Dt6.svg
[tunnckocore_newsletter]: https://badgen.net/https/liam-badge-daknys6gadky.runkit.sh/com/newsletter/tunnckocore?label&color=5199FF&icon=https://svgshare.com/i/Dt6.svg

<!-- prettier-ignore-end -->

[babylon]: https://babeljs.io/
[cacache]: https://github.com/npm/cacache
[collect-mentions]: https://github.com/olstenlarck/collect-mentions
[define-property]: https://github.com/jonschlinkert/define-property
[execa]: https://github.com/sindresorhus/execa
[fast-glob]: https://github.com/mrmlnc/fast-glob
[glob]: https://github.com/isaacs/node-glob
[globby]: https://github.com/sindresorhus/globby
[jest-runner-docs]: https://tunnckocore.com/opensource
[koa-convert]: https://github.com/gyson/koa-convert
[koa]: https://github.com/koajs/koa
[parse-github-url]: https://github.com/jonschlinkert/parse-github-url
[tiny-glob]: https://github.com/terkelg/tiny-glob
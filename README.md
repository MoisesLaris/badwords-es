# bad-words-es

A javascript filter for badwords with spanish and english words.

[![Build Status](https://travis-ci.org/web-mech/badwords.svg?branch=master)](https://travis-ci.org/web-mech/badwords)
[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg?style=flat-square)](https://github.com/semantic-release/semantic-release)

## Requirements

As of version 2, requires you either have an environment that understands ES2016 and beyond or a transpiler like Babel.

## Installation

    npm install bad-words-es --save

## Usage

```js
var Filter = require('bad-words-es'),
    filter = new Filter();

console.log(filter.clean("Don't be an ash0le")); //Don't be an ******
console.log(filter.clean("No seas pendej0")); //No seas pendej0
```

### Placeholder Overrides

```js
var Filter = require('bad-words-es');
var customFilter = new Filter({ placeHolder: 'x'});

customFilter.clean("Don't be an ash0le"); //Don't be an xxxxxx
```

### Regex Overrides

```js
var filter = new Filter({ regex: /\*|\.|$/gi });

var filter = new Filter({ replaceRegex:  /[A-Za-z0-9가-힣_]/g }); 
//multilingual support for word filtering
```

### Select language
```js
var Filter = require('bad-words-es');

//It will only filter bad words in Spanish.
var filter = new Filter({languages: ['es']});

filter.clean("Don't be an assh0le"); //Don't be an assh0le
filter.clean("Hola pendejo"); //Hola *******
```

### Add words to the blacklist

```js
var filter = new Filter(); 

filter.addWords('some', 'bad', 'word');

filter.clean("some bad word!") //**** *** ****!

//or use an array using the spread operator

var newBadWords = ['some', 'bad', 'word'];

filter.addWords(...newBadWords);

filter.clean("some bad word!") //**** *** ****!

//or

var filter = new Filter({ list: ['some', 'bad', 'word'] }); 

filter.clean("some bad word!") //**** *** ****!
```

### Instantiate with an empty list

```js
var filter = new Filter({ emptyList: true }); 
filter.clean('hell this wont clean anything'); //hell this wont clean anything
```

### Remove words from the blacklist

```js
let filter = new Filter(); 

filter.removeWords('hells', 'sadist');

filter.clean("some hells word!"); //some hells word!

//or use an array using the spread operator

let removeWords = ['hells', 'sadist'];

filter.removeWords(...removeWords);

filter.clean("some sadist hells word!"); //some sadist hells word!
```

### API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

##### Table of Contents

-   [constructor](#constructor)
-   [isProfane](#isprofane)
-   [replaceWord](#replaceword)
-   [clean](#clean)
-   [addWords](#addwords)
-   [removeWords](#removewords)

#### constructor

Filter constructor.

**Parameters**

-   `options` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Filter instance options (optional, default `{}`)
    -   `options.emptyList` **[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** Instantiate filter with no blacklist
    -   `options.list` **[array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)** Instantiate filter with custom list
    -   `options.placeHolder` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Character used to replace profane words.
    -   `options.regex` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Regular expression used to sanitize words before comparing them to blacklist.
    -   `options.replaceRegex` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Regular expression used to replace profane words with placeHolder.
    -   `options.splitRegex` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Regular expression used to split a string into words.
    -   `options.languages` **[array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)** List of the languages to use. By default it will use both Spanish and English.

#### isProfane

Determine if a string contains profane language.

**Parameters**

-   `string` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** String to evaluate for profanity.

#### replaceWord

Replace a word with placeHolder characters;

**Parameters**

-   `string` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** String to replace.

#### clean

Evaluate a string for profanity and return an edited version.

**Parameters**

-   `string` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Sentence to filter.

#### addWords

Add word(s) to blacklist filter / remove words from whitelist filter

**Parameters**

-   `word` **...[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Word(s) to add to blacklist

#### removeWords

Add words to whitelist filter

**Parameters**

-   `word` **...[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Word(s) to add to whitelist.

## Testing

    npm test

## License

The MIT License (MIT)

Copyright (c) 2022 Moisés Laris

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

# InlineResourceLiteral

InlineResource is a Javascript build tool that handles inlining of common types of resources with a declarative syntax. It provides an ability to replace pre-defined placeholders into JS expressions at build time. It automatically minifies files with extension `html` and `css`.

## Installation

Add InlineResource to the dependency by executing:
```
yarn add https://github.com/seanl-adg/InlineResourceLiteral --dev
```

## Usage

```
// source.js
...
element.innerHTML = RESOURCE_TEMPLATE;
...
```
```
// template.html
<html><div></div></html>
```
```
// build.js
const InlineResource = require("inline-resource-literal");
const fs = require('fs');

const file = fs.readFileSync('./source.js').toString();

const inlined = (new InlineResource({
    "TEMPLATE": './template.html'
})).inlineResource(file);

fs.writeFileSync('./inlined.js', inlined);
```
```
// inlined.js
element.innerHTML = "<div></div>";
```

### Inlining with Precomputed Values

```
// source.js
element.innerHTML = RESOURCE_ARGS("TEMPLATE", "DOMAIN", document.domain, "LANGUAGE", navigator.language);
```
```
// template.html
<p>domain is: RESOURCE_DOMAIN</p>
<p>language is: RESOURCE_LANGUAGE</p>
```
```
// build.js
const InlineResource = require("inline-resource-literal");
const fs = require('fs');

const file = fs.readFileSync('./source.js').toString();

const inlined = (new InlineResource({
    "TEMPLATE": './template.html'
})).inlineResource(file);

fs.writeFileSync('./inlined.js', inlined);
```
```
// inlined.js
element.innerHTML = "<p>domain is: " + document.domain + "</p>\n<p>language is: " + navigator.language + "</p>";
```

## API

Check out the [`.d.ts` file](https://github.com/seanl-adg/InlineResource/master/blob/index.d.ts).
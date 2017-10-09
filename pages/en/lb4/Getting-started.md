---
lang: en
title: 'Getting started'
keywords: LoopBack 4.0, LoopBack 4
tags:
sidebar: lb4_sidebar
permalink: /doc/en/lb4/Getting-started.html
summary:
---
## Prerequisites: JavaScript

Like other modern JavaScript frameworks (for example, Angular 2 and React) LoopBack 4 has an opinion about what flavor of JavaScript to use in your application.
The starting point is [ECMAScript 6](http://www.ecma-international.org/ecma-262/6.0/), plus the following non-standard add-ons:

 - Decorators
 - `async` / `await`
 - ES2015-modules

**All examples and snippets in the documentation use this flavor of JavaScript.**

{% include note.html content="This article will eventually cover:
- How to install the command line utility
- Using the utility to scaffold the skeleton app
- Running the app (node ., npm start)
" %}

## Installation

Make sure you have the following installed:

- Node.js >= 7.0.0
- TypeScript >= 2.0.0 `npm i -g typescript`
- TypeScript Node >= 3.0.0 `npm i -g ts-node`

## A simple example

This example creates an `Application` that responds to all HTTP requests with the text "Hello World".

### Building a LoopBack 4 application
First create a new folder.  Then, create two files within this folder: `index.ts` and `tsconfig.json`.  

{% include code-caption.html content="index.ts" %}
```js
import {Application} from '@loopback/core';
import {RestComponent, RestServer} from '@loopback/rest';

export class HelloWorldApp extends Application {
    constructor() {
      super({
        components: [RestComponent]
      });
    }
  
    async start() {
      const rest = await this.getServer(RestServer);
      rest.handler((sequence, request, response) => {
        sequence.send(response, 'Hello World');
      });
      await super.start();
      console.log(`REST server running on port: ${await rest.get('rest.port')}`);
    }
  }
  
(async function main() {
    const app = new HelloWorldApp();
    await app.start();
})();

```

Next, create a file called tsconfig.json to indicate that this is a TypeScript project and specify the TypeScript compiler options required.  For more details, see [TypeScript documentation](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html).

{% include code-caption.html content="tsconfig.json" %}
```
{
    "compilerOptions": {
      /* Basic Options */
      "target": "es6",                          
      "module": "commonjs",                     

      /* Experimental Options */
      "experimentalDecorators": true,
      "emitDecoratorMetadata": true
    }
  }
```
### Running the application

To install the required packages, enter:
```
npm install --save @loopback/core @loopback/rest
```

To run the application, enter:
```
ts-node index.ts
```

## References

For more examples and tutorials, see [Examples-and-tutorials.html](http://loopback.io/doc/en/lb4/Examples-and-tutorials.html).
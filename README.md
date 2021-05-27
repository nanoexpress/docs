---
description: Thanks for choosing nanoexpress!
---

# Getting Started

![Nano-framework for Node.js powered](.gitbook/assets/png-512-black.png)

{% hint style="info" %}
We are on [ProductHunt](https://www.producthunt.com/posts/nanoexpress) and [StackShare](https://stackshare.io/companies/nanoexpress)! Please check it out
{% endhint %}

## Coming updates and latest news at [here](https://t.me/nanoexpress)

## Features

* Express-compatible middleware\* layer
* Express-like API
* [Faster](https://github.com/the-benchmarker/web-frameworks#results) than most Node.js backend frameworks
* In-built `async` support without any of `HttpResponse` instance\*
* [Ajv](https://ajv.js.org)\* schema validator support
* [fast-json-stringify](https://github.com/fastify/fast-json-stringify)\* serialization support
* [Swagger](https://swagger.io)\* support
* In-built WebSocket support
* In-built Stream support

{% hint style="warning" %}
Code is provided as-is, do not expect or demand **free** support, warranty or debugging
{% endhint %}

## Installation

You can install 

```text
$ npm i nanoexpress
# or
$ yarn add nanoexpress
```

{% hint style="warning" %}
* This library does not support **HTTP2**!
{% endhint %}

As soon as you have installed the right package, let's create the first server

```javascript
import nanoexpress from 'nanoexpress';

const app = nanoexpress();

app.get('/', (req, res) => {
    return res.send({ status: 'ok' });
});

app.listen(3000);
```

{% hint style="info" %}
Using `app.listen(PORT, '0.0.0.0')` is recommended to use for **Docker**, **Heroku** and **AWS**
{% endhint %}


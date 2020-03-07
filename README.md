---
description: Thanks for choosing nanoexpress!
---

# Getting Started

## Features

* Express-compatible middleware layer
* [Faster](https://github.com/the-benchmarker/web-frameworks#results) than most Node.js backend frameworks
* In-built [Ajv](https://ajv.js.org) schema validator support
* In-built [fast-json-stringify](https://github.com/fastify/fast-json-stringify) serialization support
* In-built [Swagger](https://swagger.io) support
* In-built WebSocket support
* In-built Stream support
* Packed with some common **middlewares**

## Installation

{% hint style="warning" %}
Requires Node.js v12.6+.

On Node.js v12.6+ and Node.js &lt;13 for ES Modules requires argument `--experimental-modules` to be working
{% endhint %}

You can install via `npm`

{% tabs %}
{% tab title="simple" %}
```
$ npm i nanoexpress
```
{% endtab %}

{% tab title="pro" %}
```
$ npm i nanoexpress-pro
```
{% endtab %}

{% tab title="pro-slim" %}
```
$ npm i nanoexpress/pro-slim
```
{% endtab %}
{% endtabs %}

or via `yarn`

{% tabs %}
{% tab title="simple" %}
```bash
$ yarn add nanoexpress
```
{% endtab %}

{% tab title="pro" %}
```
$ yarn add nanoexpress-pro
```
{% endtab %}

{% tab title="pro-slim" %}
```
$ yarn add nanoexpress/pro-slim
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**pro** and **pro-slim** versions are licensed under GPL-3.0 license. 
{% endhint %}

{% hint style="warning" %}
* This library does not support **HTTP2**!
* **pro** and **pro-slim** versions are paid for commercial products if sources are closed
{% endhint %}

Once you're installed, let's create first server

{% tabs %}
{% tab title="simple" %}
{% code title="server.js" %}
```javascript
import nanoexpress from 'nanoexpress';

const app = nanoexpress();

app.get('/', (req, res) => {
    return res.send({ status: 'ok' });
});

app.listen(3000);
```
{% endcode %}
{% endtab %}

{% tab title="pro" %}
{% hint style="warning" %}
For CommonJS please use `cjs` suffix, example

`const nanoexpress = require('nanoexpress-pro/cjs')`
{% endhint %}

{% code title="server.js" %}
```javascript
import nanoexpress from 'nanoexpress-pro';

const app = nanoexpress();

app.get('/', (req, res) => {
    return res.send({ status: 'ok' });
});

app.listen(3000);
```
{% endcode %}
{% endtab %}

{% tab title="pro-slim" %}
{% hint style="info" %}
Difference between `pro` and `pro-slim`

* **Slim**: Less polyfilled methods, Less functionality, High performance, Low resource usage
* **Pro**: More polyfilled methods, More functionality, Mid-high performance, Mid resource usage
{% endhint %}

{% hint style="warning" %}
 `pro-slim` version supports only native Node.js ES Module powered backends. 
{% endhint %}

{% hint style="warning" %}
`pro-slim` doesn't supports sync variant. You should use [`legacyConverter`](https://github.com/nanoexpress/pro-slim/blob/master/utils/legacy.js)utility provided by `pro-slim` version.
{% endhint %}

{% code title="server.js" %}
```javascript
import nanoexpress from '@nanoexpress/pro-slim';

const app = nanoexpress();

app.get('/', async () => {
    return ({ status: 'ok' });
});

app.listen(3000);
```
{% endcode %}

### Registering listener

Registering listener ways are much more in **pro-slim** 

```typescript
app.listen(PORT: number, host?: string, is_ssl_server?: boolean)
app.listen(PORT: number[], host?: string, is_ssl_server?: boolean)
app.listen(host: string, PORT: number, is_ssl_server?: boolean)
app.listen(host: string, PORT: number[], is_ssl_server?: boolean)
app.listen(ports: Array<{ port: number, host?: string}>)
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Using `app.listen(PORT, '0.0.0.0')` is recommended to use for **Docker**, **Heroku** and **AWS**
{% endhint %}


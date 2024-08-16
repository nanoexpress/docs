# Optimizations

## Compiler optimization

Our compiler is in `Alpha` stage, so any PR or fix are welcome. Compiler improves performance for basic requests which were performed by benchmarks. But you can optimize your requests by doing some basic things. Let's go, there will be few tweaks to read.

{% hint style="danger" %}
Compiler will try to use `new Function` to execute, but if fails, to improve performance. If in your route you use some `global` functions or instances, `eval` will be used, so **SECURITY** isn't guaranteed
{% endhint %}

{% hint style="info" %}
`req.headers, req.params` only can be optimized
{% endhint %}

### Will be optimized

* `req.headers.foo`
* `req.headers["foo"]`
* `const { foo } = req.headers`

Example,

```javascript
app.get((req, res) => {
    const { origin } = req.headers; // This line will be optimized by compiler
});
```

### Will not be optimized

* `{ foo } = headers`
* `({ headers }, res) => {...}`

Example,

```javascript
app.get(({ headers }, res) => {
    // or const { headers } = req;
    const { origin } = headers; // But this line will not be optimized
});
```

## Precompile / Ahead-of-Time compile

Use `precompile` option to cache the route with entire response. Any `await` and `waits` are fired **once** as later they will be replaced with compiled content



{% hint style="warning" %}
Caveats of this kind of response:

* Does not support dynamic values
* Does not support dynamic input like `any property` of `HttpRequest`
* Does not support complex methods such as `send`, `json`
* Does not support any other types other than primitives (String, Number, Boolean only)
* Any `await` fires once while compiling
{% endhint %}

### Async example

```javascript
import { setTimeout } from 'node:timers/promises';

app.get({ precompile: true }, async (req, res) => {
    await setTimeout(5000);
    
    return res.end('string result here');
});
```

### Cache example

```javascript
app.get({ precompile: true }, (req, res) => {
    return res.end('success')
});
```

## Improve error stack trace logs

Try to call `node --enable-source-maps server.js`

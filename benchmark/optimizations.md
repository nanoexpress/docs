# Optimizations

## Performance improvement by ~25%

Try call `EXPERIMENTAL_FASTCALL=1 node server.js`

See [issue](https://github.com/uNetworking/uWebSockets.js/issues/267) for more information

## Request dumping or freeze

{% hint style="info" %}
This optimization only for **pro-slim** version
{% endhint %}

Try call `node --expose-gc server.js`

## Compiler optimization

Our compiler in `Alpha` stage, so any PR or fix are welcome. Compiler improves performance for basic requests which performed by benchmarks. But you can optimize your requests by doing some basic things. Let's go, there will be few tweaks to read.

{% hint style="danger" %}
Compiler will try to use `new Function` _\(on all versions\)_ to execute, but if fails, will try use `eval` _\(only on PRO version\)_ to improve performance. If in your route you using some `global` functions or instances, `eval` will be used, so **SECURITY** isn't guaranteed
{% endhint %}

{% hint style="info" %}
`req.headers, req.params` are only can be optimized
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

## Improve error stack trace logs

Try call `node --enable-source-maps server.js`


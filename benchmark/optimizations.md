# Optimizations

## Performance improvement by ~25%

Try call `EXPERIMENTAL_FASTCALL=1 node server.js`

See [issue](https://github.com/uNetworking/uWebSockets.js/issues/267) for more information

## Request dumping or freeze

{% hint style="info" %}
This optimization only for **pro-slim** version
{% endhint %}

Try call `node --expose-gc server.js`

## Improve error stack trace logs

Try call `node --enable-source-maps server.js`


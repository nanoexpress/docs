# Known bugs

## HTTP Pipeline not working properly

See[ this issue](https://github.com/nanoexpress/pro/issues/12)

## Routes cannot be used more than once

See [this issue](https://github.com/nanoexpress/pro/issues/12)

## Sync routes/middlewares not handled

Yes, you should read **documentation** carefully.

## Error "Invalid access of discarded ..."

Please don't forget return `HttpResponse` from route and/or middleware.

Example, `return res.send(...)` instead of `res.send(...)` at last line of route

## CORS per-route bug

{% hint style="info" %}
This bug can be fixed, bug we used this way to improve performance and reduce latency between requests
{% endhint %}

There only one workaround to this

```javascript
const corsPerRoute = cors();
app.options('/my-route', corsPerRoute);

app.get('/my-route', corsPerRoute, (req, res) => {
  res.send('this route protected by your cors per-route config');
});
```

More info can be seen at [here](https://github.com/nanoexpress/nanoexpress/issues/87)


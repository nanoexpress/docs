# Middlewares

### Built-in Middlewares

Built-in middlewares implemented at layer-level for performance reason and enables automacilly when needed, not always

{% hint style="info" %}
All of these things are already implemented in **nanoexpress**
{% endhint %}

| Alternative | Implement level | Which libraries uses |
| :--- | :--- | :--- |
| [cookie](https://github.com/jshttp/cookie) | Layer level | [cookie](https://github.com/jshttp/cookie) |
| [body-parser](https://github.com/expressjs/body-parser) | Middleware level | fast-query-parse |
| [express-ws](https://github.com/HenningM/express-ws) | Core level | [Core](https://github.com/uNetworking/uWebSockets.js) library |
| [express-serializer](https://github.com/MediaComem/express-serializer) | Middleware level | [fast-json-stringify](https://github.com/fastify/fast-json-stringify) |
| [express-ajv](https://bitbucket.org/netgenes/express-ajv) | Middleware level | [ajv](https://ajv.js.org/) |

### Middlewares

I'm excluded in-box modules from initialization for performance reason

{% hint style="warning" %}
We moved all middlewares to separate [@nanoexpress/middlewares](https://github.com/nanoexpress/middlewares) repository
{% endhint %}

### Tested Express/Connect like Middlewares

* [body-parser](https://github.com/expressjs/body-parser) \(yes, if you don't want built-in\)
* [express-fileupload](https://github.com/richardgirges/express-fileupload)
* [express-cors](https://github.com/expressjs/cors)
* [express-jwt](https://github.com/auth0/express-jwt)
* [express-session](https://github.com/expressjs/session)
* [express-graphql](https://github.com/graphql/express-graphql)
* [passport](http://www.passportjs.org)

### Basic example

```javascript
app.use((req, res, next) => {
  req.appId = 'MY_APP_ID';
  next();
});
```

### Method defining

```javascript
function lazyEnd(end) {
  setTimeout(() => this.end(end), 0);
}
app.use((req, res, next) => {
  res.lazyEnd = lazyEnd;
  next();
});
```

{% hint style="info" %}
Error which comes from **Async** Middleware automacilly will be handled by **nanoexpress**
{% endhint %}


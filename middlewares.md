# Middlewares

## Simple version

{% hint style="info" %}
**Pro** version also shares same middlewares
{% endhint %}

### Built-in Middlewares

Built-in middlewares implemented at layer-level for performance reason and enables automacilly when needed, not always

{% hint style="info" %}
All of these things are already implemented in **nanoexpress**
{% endhint %}

| Alternative | Implement level | Which libraries uses |
| :--- | :--- | :--- |
| [cookie](https://github.com/jshttp/cookie) | Layer level | [cookie](https://github.com/jshttp/cookie) |
| [body-parser](https://github.com/expressjs/body-parser) | Layer level | Node.js builtin [querystring](https://nodejs.org/api/querystring.html) |
| [express-ws](https://github.com/HenningM/express-ws) | Core level | [Core](https://github.com/uNetworking/uWebSockets.js) library |
| [express-serializer](https://github.com/MediaComem/express-serializer) | Layer level | [fast-json-stringify](https://github.com/fastify/fast-json-stringify) |
| [express-ajv](https://bitbucket.org/netgenes/express-ajv) | Layer level | [ajv](https://ajv.js.org/) |

### In-box Middlewares

I'm excluded in-box modules from initialization for performance reason

#### How-to import

```javascript
import { middlewares } from 'nanoexpress/packed';
// or import { passportInitialize } from 'nanoexpress/packed/middlewares';

const app = nanoexpress();
app.use(middlewares.passportInitialize()); // or app.use(passportInitialize());
```

**Available middlewares**

* **passport**
* **swagger-ui**
* **redoc**

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

#### You may look to [Passport](https://github.com/nanoexpress/nanoexpress/blob/master/examples/passport.js) example

{% hint style="info" %}
Error which comes from Middleware automacilly will be handled by **nanoexpress**
{% endhint %}


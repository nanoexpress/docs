# Request

## Properties

* headers
* params
* query
* body
* cookies



{% hint style="info" %}
**Tips**

* If you want your app to be faster, please consider using **schemas**
* If you do not use these properties, especially `body`, your app will response faster, because these properties parse takes time
* `req.originalUrl`, `req.baseUrl` is not the same as `express` properties, just alias to `req.url`
{% endhint %}

## Examples

### Headers example

```javascript
app.get('/secret', (req) => {
  const { authorization } = req.headers;
});
```

### Params example

```javascript
app.get('/user/:id/login', async (req) => {
  const { id } = req.params;

  const result = await db.getUser(id);

  // do something...
});
```

### Query example

```javascript
// /user?token=123
app.get('/user', async (req) => {
  const { token } = req.query;

  const result = await jwt.verifyToken(token);

  // do something...
});
```

### Body example

```javascript
app.post('/user', async (req) => {
  const { username, password } = req.body;

  // You can use db.createUser(req.body), but this may cause side-effects
  const result = await db.createUser({ username, password });

  // do something...
});
```

### Cookies example

```javascript
app.post('/user', async (req) => {
  const { userId } = req.cookies;

  // You can use db.createUser(req.body), but this may cause side-effects
  const isUserLoggedIn = await dbHelper.checkUser(userId);

  // do something...
});
```

### Get IP example

```javascript
app.get('/api/ip',(req,res) => {
    res.send({
        ip: req.getIP(),
        proxiedIP: req.getProxiedIP() // for use in production behind a reverse proxy
    });
});
```

### [Upload](https://github.com/nanoexpress/middlewares/tree/master/packages/formidable) example


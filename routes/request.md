# Request

## Properties

* headers
* params
* query
* body
* cookies

{% hint style="warning" %}
Request properties are unavailable for **pro-slim** version
{% endhint %}

{% hint style="info" %}
**Tips**

* If you want your app to be faster, please consider using **schemas**
* If you do not use these properties, especially `body`, your app will response faster, because these properties take time parse
* For **simple** and **pro** version `req.originalUrl`, `req.baseUrl` is not the same as `express` properties, just alias to `req.url`
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

{% hint style="info" %}
**Bonus!** nanoexpress handles body-parsing for you very fast
{% endhint %}

```javascript
app.post('/user', async (req) => {
  const { username, password } = req.body;

  // You can use db.createUser(req.body), but this may cause side-effects
  const result = await db.createUser({ username, password });

  // do something...
});
```

### Cookies example

{% hint style="warning" %}
Only on **Free** version!

 For working properly [cookie](https://github.com/jshttp/cookie) parsing, please install [cookie](https://github.com/jshttp/cookie) module yourself, it's in our library **peerDependencies**
{% endhint %}

```javascript
app.post('/user', async (req) => {
  const { userId } = req.cookies;

  // You can use db.createUser(req.body), but this may cause side-effects
  const isUserLoggedIn = await dbHelper.checkUser(userId);

  // do something...
});
```

### [Upload](https://github.com/nanoexpress/nanoexpress/blob/master/examples/upload-file.js) example

{% hint style="info" %}
This example uses [express-fileupload](https://github.com/richardgirges/express-fileupload) middleware as example
{% endhint %}

```javascript
const fileUpload = require('express-fileupload');
const path = require('path');

app.use(fileUpload({ useTempFiles: true }));
app.post('/', (req, res) => {
  console.debug('files', req.files);
  console.debug('body', req.body);

  req.files.file.mv(path.join(__dirname, '/uploads/file.jpg'), (err) => {
    if (err) {
      res.status(500);
      return res.send(err);
    }

    return res.send('File uploaded!');
  });
});
```


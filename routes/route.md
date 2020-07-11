---
description: This feature is available only for PRO and PRO Slim versions
---

# Route

{% hint style="danger" %}
Don't forget to return to **HttpResponse** from the route
{% endhint %}

{% hint style="info" %}
Using many middlewares may slow response performance
{% endhint %}

## Route-middleware route

```javascript
import Route from 'nanoexpress-pro/src/Route';

const route = new Route();

app.use(route);

route.get('/', async () => 'hello world');
```

{% hint style="warning" %}
if you want Route to work properly, first initialize via `app.use(routerInstance)` then registrate your routes
{% endhint %}

## Async route

### Basic Async example

```javascript
app.get('/', async () => ({ status: 'success' }));
```

### DB example

```javascript
app.get('/', async (req, res) => {
  const result = await db.getUser(req.params.id);

  return result;
});
```

### Basic example

```javascript
app.get('/', async (req, res) => {
  return res.end('hello world');
});
```

### JSON example

```javascript
app.post('/', (req, res) => {
  const { body } = req;

  res.send({ status: 'ok' });
});
```


# Route

{% hint style="danger" %}
Don't forget to return to **HttpResponse** from the route
{% endhint %}

{% hint style="info" %}
Using many middlewares may slow response performance
{% endhint %}

## Route-middleware route

{% tabs %}
{% tab title="ESM" %}
```javascript
import Route from 'nanoexpress/src/Route';

const route = new Route();

app.use(route);

route.get('/', async () => 'hello world');
```
{% endtab %}

{% tab title="CJS" %}
```javascript
const Route = require('nanoexpress/cjs/Route');

const route = new Route();

app.use(route);

route.get('/', async () => 'hello world');
```
{% endtab %}
{% endtabs %}

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

  return res.send({ status: 'ok' });
});
```

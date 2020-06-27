# Static serve

{% hint style="info" %}
See [here](https://github.com/nanoexpress/middlewares/tree/master/static) for examples and docs

You can try [@expressjs/serve-static](https://github.com/expressjs/serve-static) + legacy middleware converter \(see [here](../middlewares.md)\)
{% endhint %}

{% tabs %}
{% tab title="CommonJS" %}
```javascript
const nanoexpress = require('nanoexpress-pro/cjs');
const staticServe = require('@nanoexpress/middlewares/static/cjs');
const path = require('path');

const app = nanoexpress();

app.use(staticServe(path.join(__dirname, 'static')));

app.listen(8000);
```
{% endtab %}

{% tab title="ES Module" %}
```javascript
import nanoexpress from 'nanoexpress-pro';
import staticServe from '@nanoexpress/middlewares/static';
import path from 'path';

const app = nanoexpress();

app.use(staticServe(path.resolve('./static')));

app.listen(8000);
```
{% endtab %}
{% endtabs %}


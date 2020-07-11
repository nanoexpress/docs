# Static serve

{% hint style="info" %}
The **pro-slim** version doesn't support _static serving_, but can be added via **middlewares** and/or **defines**

You can try [@expressjs/serve-static](https://github.com/expressjs/serve-static) + legacy middleware converter \(see [here](../middlewares.md)\)
{% endhint %}

{% tabs %}
{% tab title="CommonJS" %}
```javascript
const nanoexpress = require('nanoexpress-pro/cjs');
const staticServe = require('nanoexpress/cjs/static');
const path = require('path');

const app = nanoexpress();

app.use(staticServe(path.join(__dirname, 'static')));

app.listen(8000);
```
{% endtab %}

{% tab title="ES Module" %}
```javascript
import nanoexpress from 'nanoexpress-pro';
import staticServe from 'nanoexpress/src/static';
import path from 'path';

const app = nanoexpress();

app.use(staticServe(path.join(__dirname, 'static')));

app.listen(8000);
```
{% endtab %}
{% endtabs %}


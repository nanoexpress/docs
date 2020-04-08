# Schemas

> ## Swagger documentation generated based on schemas

{% hint style="warning" %}
This feature isn't available for **pro-slim** version
{% endhint %}

{% hint style="info" %}
If you correctly and exactly define the schema, your app will be faster by 25-30% which is good and validation support will be out-of-the-box
{% endhint %}

{% hint style="info" %}
On **free** version:

For its working, please install [Ajv](http://ajv.js.org/) module yourself, it's in our library in **peerDependencies**
{% endhint %}

## Validation

{% hint style="info" %}
All validations are optional
{% endhint %}

### Types of validation

* headers
* params
* query
* body
* cookies

{% hint style="info" %}
For more information, please look at [Ajv docs](http://ajv.js.org/)
{% endhint %}

{% hint style="info" %}
If you don't want to use any or all \(except **body**\) of these validation methods, please set it to **false** for performance reason
{% endhint %}

```javascript
app.get(
  '/',
  {
    schema: {
      headers: {
        type: 'object',
        properties: {
          authorization: { type: 'string' }
        }
      },
      query: false,
      params: false,
      cookies: false
    }
  },
  async () => ({ hello: 'world' })
);

app.listen(4000);
```

## Serialization

### Types of serialization

{% hint style="info" %}
For better performance and working serialization, please install [fast-json-stringify](https://github.com/fastify/fast-json-stringify) module yourself, it's in our library in **peerDependencies**
{% endhint %}

We use [fast-json-stringify](https://github.com/fastify/fast-json-stringify) under the hood for serialization and improving response time \(applies for **Array** and **Object**\)

{% hint style="warning" %}
If schema is wrong, error is not causing, it just removes that value from response which may be bad for your application, so, please be careful when typing schema
{% endhint %}

{% hint style="info" %}
If **required** property was used and value doesn't return, server may crash or performance may be dropped by **6-8 times**, please, try to make sure everything is correct on your **schema**
{% endhint %}

**Response content types**: 

* `response`
* `response.HTTP_CODE`

{% hint style="info" %}
You can see discussion about this [here](https://github.com/fastify/fast-json-stringify/issues/169) and [here](https://github.com/fastify/fast-json-stringify/pull/172), you can submit PR with your solution. Your PR may help to improve this library and other ~2K app performance
{% endhint %}

```javascript
app.get(
  '/',
  {
    schema: {
      response: {
        type: 'object',
        properties: {
          hello: { type: 'string' }
        }
      }
    }
  },
  async () => ({ hello: 'world' })
);

app.listen(4000);
```

### **HTTP Code-based serialization**

```javascript
app.get(
  '/',
  {
    schema: {
      response: {
        200: {
          type: 'object',
          properties: {
            hello: { type: 'string' }
          }
        },
        404: {
          type: 'object',
          properties: {
            status: { type: 'string' }
          }
        }
      }
    }
  },
  async () => ({ hello: 'world' })
);

app.listen(4000);
```


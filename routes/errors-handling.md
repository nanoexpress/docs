# Errors handling

{% hint style="info" %}
Node.js v13.5+ new argument params help you trace warnings and errors

* `--trace-uncaught`
* `--trace-warnings`

Example, `node --trace-uncaught server.js`
{% endhint %}

## Error handling

{% hint style="warning" %}
Only **async** route functions and middlewares are handled
{% endhint %}

```typescript
app.setErrorHandler(
  (err: Error, req: HttpRequest, res: HttpResponse): HttpResponse => {
    if (checkSomething(err)) {
      return res.send({
        status: 'error',
        status_code: 500,
        message: 'oops'
      })
    }
  }
);
```

{% swagger baseUrl="http://localhost:8000" path="/error-route" method="get" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="" type="string" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

## Not found handler

```typescript
app.setNotFoundHandler((req: HttpRequest, res: HttpResponse): HttpResponse => {
    return res.send({ code: 404, message: 'You entered wrong url' });
});
```

{% swagger baseUrl="http://localhost:8000" path="/anyUrl" method="get" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="" type="string" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

## Validation error handler

{% hint style="warning" %}
Validation error handler unavailable for **pro-slim** version
{% endhint %}

```typescript
app.setValidationErrorHandler((errors: AjvValidationErrors[], req: HttpRequest, res: HttpResponse): HttpResponse => {
    return res.json({ errors });
});
```

{% swagger baseUrl="http://locahost:8000" path="/validate-error" method="get" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="foo" type="string" %}
bar
{% endswagger-parameter %}

{% swagger-response status="400" description="" %}
```
{
  "errors": {
    "type": "errors",
    "errors": [
      {
        "body": ["type should be string, but got ..."]
      }
    ]
  }
}
```
{% endswagger-response %}
{% endswagger %}

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

{% api-method method="get" host="http://localhost:8000" path="/error-route" %}

## Not found handler

```typescript
app.setNotFoundHandler((req: HttpRequest, res: HttpResponse): HttpResponse => {
    return res.send({ code: 404, message: 'You entered wrong url' });
});
```

{% api-method method="get" host="http://localhost:8000" path="/anyUrl" %}

## Validation error handler

{% hint style="warning" %}
Validation error handler unavailable for **pro-slim** version
{% endhint %}

```typescript
app.setValidationErrorHandler((errors: AjvValidationErrors[], req: HttpRequest, res: HttpResponse): HttpResponse => {
    return res.json({ errors });
});
```

{% api-method method="get" host="http://locahost:8000" path="/validate-error" %}
{% api-method-summary %}

{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="foo" type="string" required=false %}
bar
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text
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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}


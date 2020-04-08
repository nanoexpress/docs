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

{% tabs %}
{% tab title="simple & pro" %}
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
{% endtab %}

{% tab title="pro-slim" %}
```typescript
interface ErrorHandlerResponse {
  status!: 'success' | 'error';
  status_code?: number; // response status code in `int` format
  stack_trace?: string; // error stack trace
  message!: string;
  code?: string; // auth_failed, bad_request, ...
}
app.setErrorHandler(
  (err: Error): ErrorHandlerResponse => {
    if (checkSomething(err)) {
      return {
        status: 'error',
        status_code: 500,
        message: 'oops'
      }
    }
  }
);
```
{% endtab %}
{% endtabs %}

{% api-method method="get" host="http://localhost:8000" path="/error-route" %}
{% api-method-summary %}
Error handling example
{% endapi-method-summary %}

{% api-method-description %}
Example of error handled request
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
  "status": "error",
  "status_code": 500,
  "message": "oops"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Not found handler

{% tabs %}
{% tab title="simple" %}
```typescript
app.setNotFoundHandler((res: HttpResponse, req: HttpRequest): HttpResponse => {
    return res.send({ code: 404, message: 'You entered wrong url' });
});
```
{% endtab %}

{% tab title="pro" %}
```typescript
app.setNotFoundHandler((req: HttpRequest, res: HttpResponse): HttpResponse => {
    return res.send({ code: 404, message: 'You entered wrong url' });
});
```
{% endtab %}

{% tab title="pro-slim" %}
```typescript
app.setNotFoundHandler(async (req: HttpRequest, res: HttpResponse): Promise<HttpResponse> => {
    return res.send({ code: 404, message: 'You entered wrong url' });
});
```
{% endtab %}
{% endtabs %}

{% api-method method="get" host="http://localhost:8000" path="/anyUrl" %}
{% api-method-summary %}
Not found example
{% endapi-method-summary %}

{% api-method-description %}
Example of any not found error
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
  "code": 404,
  "message": "You entered wrong url"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

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
Validation error example
{% endapi-method-summary %}

{% api-method-description %}
Example of body validation error
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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}


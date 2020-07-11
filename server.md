# Server

## Options

```typescript
{
swagger: SwaggerObject,
configureAjv(ajv: Ajv): AjvConfigured,
https: {
    key_file_name: string,
    cert_file_name: string,
    passphrase: string
  },
console: CustomConsole {
    log: function,
    error: function
  }
}
```

## Instance methods

* `app.get(req, res)`
* `app.post(req, res)`
* `app.put(req, res)`
* `app.patch(req, res)`
* `app.del(req, res)`
* `app.head(req, res)`
* `app.trace(req, res)`

Special routes are

* `app.ws(req, ws)`
* `app.any(req, res)`
* `app.options(req, res)`


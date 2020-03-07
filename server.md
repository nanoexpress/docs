# Server

## Options

### Simple version

{% hint style="info" %}
**Pro** version also shares same options
{% endhint %}

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

### Pro Slim version

```typescript
{
isSSL: boolean,
https: {
    key_file_name: string,
    cert_file_name: string,
    passphrase: string,
    separateServer: number | boolean = 443
  },
console: CustomConsole {
    log: function,
    error: function
  },
json_spaces: number
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

Special route are

* `app.ws(req, ws)`
* `app.any(req, res)`
* `app.options(req, res)`


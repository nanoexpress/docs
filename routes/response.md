# Response

## [uWebSockets.js](https://github.com/uNetworking/uWebSockets.js) methods

See [here](https://unetworking.github.io/uWebSockets.js/generated/interfaces/httpresponse.html)

## Implemented methods

{% tabs %}
{% tab title="simple" %}
* send
* json _\(same as send, but for compatibility we keep this method\)_
* sendFile
* redirect
* status
* writeHead
* cookie
* setCookie
* hasCookie
* removeCookie
* setHeader
* getHeader
* hasHeader
* removeHeader
* setHeaders
* writeHeaderValues
* writeHeaders
* type
* header
{% endtab %}

{% tab title="pro" %}
All methods of **free** version, plus

* pipe
{% endtab %}

{% tab title="pro-slim" %}
{% hint style="warning" %}
Cookie methods are unavailable for **pro-slim** version
{% endhint %}

* pipe
* send
* sendFile
* compressStream
* redirect
* status
* writeHead
* setHeader
* getHeader
* hasHeader
* removeHeader
* setHeaders
* writeHeaderValues
* writeHeaders
* type
* header
{% endtab %}
{% endtabs %}

## Examples

### Cookie + JSON example

```javascript
app.get('/is_logged', async (req, res) => {
  const status = res.hasCookie('userId') ? 'success' : 'error';

  res.send({ status });
});
```

### Redirect + Params example

```javascript
app.get('/user/:id/login', async (req, res) => {
  const { id } = req.params;

  const result = await db.getUser(id);

  return res.redirect(`/user/${id}/`);
});
```

### sendFile

{% hint style="info" %}
File should be on same path where JS file or you can try **Absolute path** for **stream/sendFile**
{% endhint %}

```javascript
app.get('/video.mp4', async (req, res) => {
  return res.sendFile('video.mp4');
});
```


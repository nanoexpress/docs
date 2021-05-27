# Response

## [uWebSockets.js](https://github.com/uNetworking/uWebSockets.js) methods

See [here](https://unetworking.github.io/uWebSockets.js/generated/interfaces/httpresponse.html)

## Implemented methods

* send
* pipe
* json \(same as send, but for compatibility we keep this method\)
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

## Examples

### Cookie + JSON example

```javascript
app.get('/is_logged', async (req, res) => {
  const status = res.hasCookie('userId') ? 'success' : 'error';

  return res.send({ status });
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
File should be on the same path where JS file is or you can try **Absolute path** for **stream/sendFile**
{% endhint %}

```javascript
app.get('/video.mp4', async (req, res) => {
  return res.sendFile('video.mp4');
});
```


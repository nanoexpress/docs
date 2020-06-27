# WebSocket

## Options

```javascript
{
    maxPayloadLength: number = 16 * 1024 * 1024,
    idleTimeout: number = 120,
    compression: number = 0,
    maxBackpressure: number = 0
}
```

{% hint style="info" %}
See more about options [here](https://unetworking.github.io/uWebSockets.js/generated/interfaces/websocketbehavior.html)
{% endhint %}

### Basic example

```javascript
app.ws('/ws', (req, res) => {
  console.log('Connecting...');

  res.on('connection', (ws) => {
    console.log('Connected');

    ws.on('message', (msg) => {
      console.log('Message received', msg);
      ws.send(msg);
    });
    ws.on('close', (code, message) => {
      console.log('Connection closed', { code, message });
    });
  });
  res.on('upgrade', () => {
    console.log('Connection upgrade');
  });
});
```

### Raw example

{% hint style="warning" %}
Any polyfilled methods are unavailable here, But performance will be faster due to less layer cost.
{% endhint %}

```javascript
app.ws('/', { isRaw: true }, (req, res) => {
  res.on('connection', (ws) => {
    // do something...
  });
});
```

### Schema example

{% hint style="info" %}
This option auto-parses JSON-strings such as **Array** and **Objects** which may be helpful.
{% endhint %}

```javascript
app.ws(
  '/',
  {
    schema: {
      type: 'object',
      properties: {
        type: { type: 'string' },
        action: { type: 'string' }
      }
    }
  },
  (req, res) => {
  res.on('connection', (ws) => {
    ws.on('message', ({ type, action }) => {
      ws.send(
        JSON.stringify({
          state: 'send-back',
          type,
          action
        })
      );
    });
    });
  }
);
```

{% hint style="info" %}
Using **schema** option may improve safety by validating messages and gives you auto-parsing of messages
{% endhint %}


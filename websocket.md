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

{% hint style="warning" %}
**Pro** version also shares same options
{% endhint %}

### Basic example

```javascript
app.ws('/', (req, ws) => {
  console.log('Connected');

  ws.on('message', (message) => {
    console.log('Message received', message);
  });
});
```

### Raw example

{% hint style="warning" %}
Any polyfilled methods unavailable here, But performance will be faster due of less layer cost. 

This option only for **free** and **pro** versions
{% endhint %}

```javascript
app.ws('/', { isRaw: true }, (req, ws) => {
  // do something...
});
```

### Schema example

{% hint style="info" %}
This option auto-parses JSON-strings such as **Array** and **Objects** which may be helpful.

This option only for **free** and **pro** versions
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
  (req, ws) => {
    ws.on('message', ({ type, action }) => {
      ws.send(
        JSON.stringify({
          state: 'send-back',
          type,
          action
        })
      );
    });
  }
);
```

{% hint style="info" %}
Using **schema** option may improve safety by validating messages and gives you auto-parsing of messages
{% endhint %}




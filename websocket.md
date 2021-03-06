# WebSocket

## Options

{% hint style="info" %}
See more about options [here](https://unetworking.github.io/uWebSockets.js/generated/interfaces/websocketbehavior.html)
{% endhint %}

### Exposed example

```javascript
import { exposeWebSocket } from 'nanoexpress/exposes/index.js';

app.ws('/ws', (req, res) => exposeWebSocket({
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
}));
```

### Basic example

{% hint style="warning" %}
Any polyfilled methods are unavailable here, But performance will be faster due to less layer cost.
{% endhint %}

```javascript
app.ws('/', {
  /* Options */
  compression: uWS.SHARED_COMPRESSOR,
  maxPayloadLength: 16 * 1024 * 1024,
  idleTimeout: 10,
  /* Handlers */
  open: (ws) => {
    console.log('A WebSocket connected!');
  },
  message: (ws, message, isBinary) => {
    /* Ok is false if backpressure was built up, wait for drain */
    let ok = ws.send(message, isBinary);
  },
  drain: (ws) => {
    console.log('WebSocket backpressure: ' + ws.getBufferedAmount());
  },
  close: (ws, code, message) => {
    console.log('WebSocket closed');
  }
});
```


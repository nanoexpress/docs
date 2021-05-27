# Known bugs

## HTTP Pipeline not working properly

See[ this issue](https://github.com/nanoexpress/pro/issues/12)

## Routes cannot be used more than once

See [this issue](https://github.com/nanoexpress/pro/issues/12)

## Sync routes/middlewares not handled

Yes, you should read **documentation** carefully.

## Error "Invalid access of discarded ..."

Please don't forget return `HttpResponse` from route and/or middleware.

Example, `return res.send(...)` instead of `res.send(...)` at last line of route


# Benchmark

{% hint style="warning" %}
Multi-threading/Clustering is available in Linux-only env
{% endhint %}

{% hint style="info" %}
Docker may be a good place to get started with Clustering. But remember, on real Linux results are always higher than on server Docker container by 5-10%
{% endhint %}

{% hint style="info" %}
In this benchmark all framework/libraries was used as basic example without any middleware, when you use any middlewares or you already have complex logic, try to optimize them to improve performance as this can slow down RPS. We cannot guarantee any performance improvements on complex backend applications
{% endhint %}

**Benchmark command**: `wrk -t2 -d2` or `wrk TEST_URL`

You can see live benchmark results at [here](https://github.com/the-benchmarker/web-frameworks#results)

**nanoexpress** fastest Node.js backend framework yet existing and existed around the world in the history and exists in the list of TOP 20 fastest backend framework over all languages

> in reality fastest Node.js backend framework is **uWebSockets.js**, but it's doesn't includes middleware mechanism for easier and faster development. If you Expert/PRO-level developer, i'm recommend you using **uWebSockets.js** instead of nanoexpress due of unbeatable performance around Node.js ecosystem

## Machines

### MBP Mid-2012

* OS: macOS Catalina
* CPU: i5-3210M
* Memory: 8GB DDR3 1600Mhz
* Env: macOS itself
* Clustering: unavailable

| Library | Req/sec | Memory |
| :--- | :--- | :--- |
| uWebSockets.js | ~70K | ~4Mb |
| nanoexpress Pro Slim | ~70K | ~8Mb |
| nanoexpress Pro | ~60K | ~18Mb |
| nanoexpress | ~55K | ~12Mb |
| Raw HTTP | ~35K | ~29Mb |
| express | ~25K | ~43Mb |

### Dev Machine

* OS: ElementaryOS 5.1
* CPU: i9-9900K 5Ghz
* Memory: 64GB DDR4 3000Mhz
* Env: Linux
* Clustering: available \(on 16 threads\)

Note: more than 4-cores aren't used at unknown reason, but it should improve performance even marginally

| Library | Req/sec | Memory |
| :--- | :--- | :--- |
| uWebSockets.js | ~400K | ~14Mb |
| nanoexpress Pro Slim | ~400K | ~19Mb |
| nanoexpress Pro | ~350K | ~26Mb |
| nanoexpress | ~300K | ~22Mb |
| Raw HTTP | ~250K | ~40Mb |
| express | ~200K | ~70Mb |

## Why

and when to use this framework for my backend application?

1. When you want to reduce server cost for WebSocket and/or WebRTC real-time comminucation and file-exchange \(maybe stream, video, photo, etc\) servers.
2. When your server has low RAM memory
3. Your logic is easy and simple
4. Startups which looks for faster startup
5. You want to try out how it works?!
6. You don't want to spend a lot for servers

Example for HTTP

> 5$ DigitalOcean plan can handle ~1M HTTP Requests per day easily and without any slowdowns

or for WebSocket

> 5$ DigitalOcean plan can handle ~10M Downloads per month in torrent server easily


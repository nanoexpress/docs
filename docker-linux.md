# Docker / Linux

{% hint style="info" %}
If you use **alpine** or **slim** version of **node** images, some errors may happen and you can fix with this minimal guide
{% endhint %}

## Requires

* git

## Errors

### For `git` missing error

```text
# FROM ...
RUN apk add --no-cache git
# your scripts
```

### For `Alpine` incompatible error

```text
# your scripts
RUN ln -s /lib/libc.musl-x86_64.so.1 /lib/ld-linux-x86-64.so.2

# your commands
# CMD ["node", "server.js"]
```

### For CentOS 7 `glibc 2.18` not found error

First, please try

```text
# FROM ...
RUN apk add --no-cache gcompat
# your scripts
```

or try

```text
# FROM ...
RUN apk add --no-cache libc6-compat
RUN mv /lib64/ld-linux-x86-64.so.2 /lib
# your scripts
```

{% hint style="info" %}
If these solutions didn't work, try solutions from [here](https://serverfault.com/a/894689) and [here](https://serverfault.com/a/980302)
{% endhint %}

### Multi-thread / Cluster

Clustering is available on **Linux**, if your OS isn't Linux, you can try **Docker** as it works on **Docker Linux** container


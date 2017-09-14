# Cervical Spine

A seamless port from [Spinal](https://github.com/jitta/spinal) broker architecture to broker-less DNS-based microservice architecture

This library is used as an intention to remove broker from the system and use HTTP call to DNS-based services instead. Common use-case is [Docker Swarm](https://docs.docker.com/engine/swarm/) and [Kubernetes](https://kubernetes.io/).

Just remove spinal and install cervical-spine instead.

```
npm install cervical-spine
```

Then, replace each `require('spinal')` to `require('cervical-spine')`.

## How it works

Cervical Spine has same API calls with Spinal. For example, when you call `user.get` with an argument `{"id":"1"}` it will send a HTTP POST request to `http://user:7557/` with data `{"name":"get","data":{"id":1}}`.

You can also specify host prefix and suffix by assigning env variable `SPINAL_HOSTNAME_PREFIX` and `SPINAL_HOSTNAME_SUFFIX`. Alternatively passing an option `hostname_prefix` and `hostname_prefix` when initializing a spinal node. For example, having `SPINAL_HOSTNAME_PREFIX=production- SPINAL_HOSTNAME_SUFFIX=-service` will make a call to `http://production-user-service:7557/`

Caching still works by passing `redis` options at node initialization instead of broker in Spinal.
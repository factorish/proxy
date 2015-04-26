Factorish Proxy
===============

About
-----

Factorish Proxy is a lightweight ( < 30mb ) container based on `gliderlabs/alpine` with nginx running as a http load balancer.  It uses data collected from `gliderlabs/registrator` to create load-balancing pools for the specified services by writing out an `nginx.conf` using the `confd` templating engine.

It's very simple to use, you simply pass in the `etcd` endpoint to connect to and list the services that you which to subscribe to and the port you want to proxy for it.

Example
-------

You're running a docker registry backed by `s3` and wish to load balance them.  You're aready running registrator and your etcd services look like this:

```
$ etcdctl ls /services  --recursive
/services/registry/core-01:factorish-registry:5000
/services/registry/core-02:factorish-registry:5000
/services/registry/core-03:factorish-registry:5000
```

We simply need to tell factorish-proxy the etcd endpoint to connect to and provide it the name of the service ( in this case registry ) and the port to load balance it on via an environment variable `-e registry=8080`.

```
$ docker run -d -p 8080:8080 -e registry=8080 \
  -e ETCD_HOST=$COREOS_PRIVATE_IPV4 \
  --name factorish-proxy factorish/proxy
```

You can balance as many services as you want by simply adding more of these variables.


Author(s)
======

Paul Czarkowski (paul@paulcz.net)

License
=======

Copyright 2014 Paul Czarkowski

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

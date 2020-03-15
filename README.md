# k8s-overwrite-header-demo

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![GitHub issues open](https://img.shields.io/github/issues/ibara1454/k8s-overwrite-header-demo.svg?maxAge=2592000)](https://github.com/ibara1454/k8s-overwrite-header-demo/issues)
[![License: MIT](https://img.shields.io/badge/kubernetes-v1.13.25-green)](https://v1-13.docs.kubernetes.io/docs/setup/release/notes/)

This is a demo to show how to overwrite / append HTTP headers to request.

## Feature

- Return a `text/plain` response which contains all HTTP request headers.
- Any request to `/overwrite` which `Content-Type` header will be overwriten by `application/json`.

## Usage

### Applying resources

Clone the resource config files and apply to the cluster.

Notice: In this sample, we use [GKE](https://cloud.google.com/kubernetes-engine?hl=ja) for constructing kubernetes cluster.
You should check your cluster provider supports use of *ingress*.

```bash
# Clone this repository
$ git clone https://github.com/ibara1454/k8s-overwrite-header-demo.git
# Change current directory to such repository
$ cd k8s-overwrite-header-demo
# Apply all resource config files (to current namespace)
$ kubectl apply -f .
```

### Verification

Get the external IP address of cluster by using `kubectl get ingress`.

```bash
$ kubectl get ingress
# NAME      HOSTS   ADDRESS           PORTS   AGE
# ingress   *       130.211.***.***   80      108s
```

Access to `/` of the external IP. This is a normal pattern.

```bash
$ curl 130.211.***.*** | jq
# {
#   "host": "node-clusterip",
#   "connection": "close",
#   "user-agent": "curl/7.58.0",
#   "accept": "*/*"
# }
```

Access to `/overwrite` of the external IP. You could see an additional `"content-type": "application/json"` is appended.

```bash
$ curl 130.211.***.***/overwrite | jq
# {
#   "content-type": "application/json",
#   "host": "node-clusterip",
#   "connection": "close",
#   "user-agent": "curl/7.58.0",
#   "accept": "*/*"
# }
```

### Deleting resources

After verification, you might want to delete all resources just by using `kubectl delete`.

```bash
kubectl delete -f .
```

## License

The MIT License (MIT).
Copyright (c) 2020, Chiajun Wang

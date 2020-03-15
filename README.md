# k8s-overwrite-header-demo

This is a demo to show how to overwrite / append HTTP headers to request.

## Feature

- Return a `text/plain` response which contains all HTTP request headers.
- Any request to `/overwrite` which `Content-Type` header will be overwriten by `application/json`.

## Usage

### Applying resources

```bash
# Clone this repository
git clone https://github.com/ibara1454/k8s-overwrite-header-demo.git
# Change current directory to such repository
cd k8s-overwrite-header-demo
# Apply all resource config files (to current namespace)
kubectl apply -f .
```

### Deleting resources

```bash
kubectl delete -f .
```

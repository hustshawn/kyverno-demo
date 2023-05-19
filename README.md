kyverno-demo
===
This is a demo to see how kyverno works. We are targeting to limit any workload applied to the cluster should be request less than `3` CPU.

## Steps
1. Install `kyverno` as mentioned in [offical doc](https://kyverno.io/docs/installation/)
2. Create the `cluster-policy`
```
kubectl apply -f cluster-policy.yaml
```
3. Create the test workload
```
kubectl apply -f inflate.yaml
```

The result looks like below. The request was rejected, since we limit the CPU not greater than 2.
```
# kubectl apply -f inflate.yaml
Error from server: error when creating "inflate.yaml": admission webhook "validate.kyverno.svc-fail" denied the request:

policy Deployment/scaling-demo/inflate for resource violation:

limit-cpu-request:
  limit-cpu-request: 'validation error: CPU request should not exceed 2. rule limit-cpu-request
    failed at path /spec/template/spec/containers/0/resources/requests/cpu/'
```

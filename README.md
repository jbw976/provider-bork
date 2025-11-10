# provider-bork

`provider-bork` is a terrible [Crossplane](https://crossplane.io/) Provider
that is meant to cause problems with its `BorkResource`:

```yaml
apiVersion: bork.crossplane.io/v1alpha1
kind: BorkResource
metadata:
  name: doh-bork
  namespace: default
spec:
  forProvider:
    borkValue: 2
    dataValue: 1
```

You can set the `dataValue` to whatever you want, but the provider will
reconcile the `BorkResource` and set that `dataValue` to the `borkValue`
instead. This can cause chaos when a `BorkResource` is composed as part of a
composite resource (XR), as the XR and `provider-bork` rapidly fight over the
`dataValue` field. Fun times!

This is a good demo and test of the XR circuit breaker funcitonality.
# local-path-provisioner zarf package

OCI component for the [Rancher Local Path Provisioner](https://github.com/rancher/local-path-provisioner)

## Try it out

```
kind: ZarfPackageConfig
metadata:
  name: example-package
  description: "example package"
  version: 0.0.1

components:
  - name: local-path-provisioner
    required: true
    import:
      url: oci://ghcr.io/brandtkeller/zarf/local-path-provisioner:0.0.1-skeleton
      name: local-path-provisioner
```

## Considerations
This component contains some global context resources and is not currently capable to be deployed multiple times in the same cluster.
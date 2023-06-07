# nextcloud zarf component

OCI component for [nextcloud]()

## Try it out

```
kind: ZarfPackageConfig
metadata:
  name: example-package
  description: "example package"
  version: 0.0.1

components:
  - name: nextcloud
    required: true
    import:
      url: oci://ghcr.io/brandtkeller/zarf/nextcloud:0.0.1-skeleton
      name: nextcloud
```

## Considerations
This component contains some global context resources and is not currently capable to be deployed multiple times in the same cluster.
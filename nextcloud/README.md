# nextcloud zarf component

OCI component for [nextcloud]()

## Important notes
Auth issue with the bitnami oci charts. Currently pulling locally and including via `localPath`

`helm pull oci://registry-1.docker.io/bitnamicharts/postgresql --version <version> --untar`

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
      url: oci://ghcr.io/brandtkeller/zarf/nextcloud:4.1.0-skeleton
      name: nextcloud
```

## Considerations
This component contains some global context resources and is not currently capable to be deployed multiple times in the same cluster.
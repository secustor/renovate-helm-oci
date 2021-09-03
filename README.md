# renovate-helm-oci

There is a library chart which acts as a template chart for app1 and app2.

In the [Chart.yaml](https://github.com/ankitabhopatkar13/renovate-helm-oci/blob/main/app1/Chart.yaml#L26) of app1, I have added a dependency pointing to the OCI registry of Github and on my local when I perform a login to that registry, I am able to do a `helm dependency update` which essentially pulls from the Github package registry.

When I am trying to run renovate on app1, app2 helm charts, renovate fails with the error - 

```
"err": {
         "name": "UnsupportedProtocolError",
         "message": "Unsupported protocol \"oci:\"",
```

Dependencies are defined as -

```
dependencies:
- name: library
  version: 0.1.0
  repository: oci://ghcr.io/ankitabhopatkar13/library
  import-values:
    - defaults
```

Reference: https://helm.sh/docs/topics/registries/#specifying-dependencies

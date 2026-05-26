# mosparo

A Helm chart for mosparo

This chart was created from the docker-compose.yaml example with the great tool [Katenary](https://github.com/metal3d/katenary) (v3 pre release) and adjusted manually: shared RWX-Volume, network policy

## Adding the Helm Repository

Add the mosparo Helm repository to your local Helm installation:

```bash
helm repo add mosparo https://helm.mosparo.io
helm repo update
```

_The Helm repository is hosted on GitHub Pages._

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
# Standard install
helm upgrade --install my-release mosparo/mosparo

# With a custom namespace (created if it doesn't exist)
helm upgrade --install my-release mosparo/mosparo --namespace my-namespace --create-namespace

# With a custom values file
helm upgrade --install my-release mosparo/mosparo -f my-values.yaml
```

See the [Helm documentation](https://helm.sh/docs/intro/using_helm/) for more information on installing and managing the chart.

## Upgrading

### 0.3.x -> 0.4.0 (breaking change)

The `mosparoweb.ingress` block has been moved under a new `mosparoweb.expose` node
to allow switching between a Kubernetes `Ingress` and a Gateway API `HTTPRoute`.

Migration:

| Old (<= 0.3.x)                        | New (>= 0.4.0)                             |
|---------------------------------------|--------------------------------------------|
| `mosparoweb.ingress.enabled: true`    | `mosparoweb.expose.type: ingress` (default)|
| `mosparoweb.ingress.enabled: false`   | `mosparoweb.expose.type: none`             |
| `mosparoweb.ingress.host`             | `mosparoweb.expose.ingress.host`           |
| `mosparoweb.ingress.path`             | `mosparoweb.expose.ingress.path`           |
| `mosparoweb.ingress.class`            | `mosparoweb.expose.ingress.class`          |
| `mosparoweb.ingress.annotations`      | `mosparoweb.expose.ingress.annotations`    |

To use a Gateway API `HTTPRoute` instead of an `Ingress`:

```yaml
mosparoweb:
  expose:
    type: route
    route:
      parentRefs:
        - name: public
          namespace: gateway-system
          sectionName: https
      hostnames:
        - "mosparo.example.com"
```

Requires the Gateway API CRDs (`gateway.networking.k8s.io/v1`) to be installed in the cluster.

## Configuration

See the values.yaml file for all configurable parameters.

The following table lists the configurable parameters of the mosparo chart and their default values.

| Parameter                                                | Default            |
|----------------------------------------------------------|--------------------|
| `db.environment.MYSQL_PASSWORD`                          | `mosparo_password` |
| `db.environment.MYSQL_ROOT_PASSWORD`                     | `mosparo_root_pw`  |
| `db.imagePullPolicy`                                     | `IfNotPresent`     |
| `db.persistence.dbdata.accessMode[0].value`              | `ReadWriteOnce`    |
| `db.persistence.dbdata.enabled`                          | `true`             |
| `db.persistence.dbdata.size`                             | `1Gi`              |
| `db.persistence.dbdata.storageClass`                     | `-`                |
| `db.replicas`                                            | `1`                |
| `db.repository.image`                                    | `mariadb`          |
| `db.repository.tag`                                      | `10.10`            |
| `db.serviceAccount`                                      | ``                 |
| `mosparoweb.expose.type`                                 | `ingress`          |
| `mosparoweb.expose.ingress.annotations`                  | `{}`               |
| `mosparoweb.expose.ingress.class`                        | `-`                |
| `mosparoweb.expose.ingress.host`                         | ``                 |
| `mosparoweb.expose.ingress.path`                         | `/`                |
| `mosparoweb.expose.route.annotations`                    | `{}`               |
| `mosparoweb.expose.route.parentRefs`                     | `[]`               |
| `mosparoweb.expose.route.hostnames`                      | `[]`               |
| `mosparoweb.imagePullPolicy`                             | `Always`           |
| `mosparoweb.persistence.mosparodata.accessMode[0].value` | `ReadWriteMany`    |
| `mosparoweb.persistence.mosparodata.enabled`             | `true`             |
| `mosparoweb.persistence.mosparodata.size`                | `1Gi`              |
| `mosparoweb.persistence.mosparodata.storageClass`        | `-`                |
| `mosparoweb.replicas`                                    | `1`                |
| `mosparoweb.repository.image`                            | `mosparo/mosparo`  |
| `mosparoweb.repository.tag`                              | `latest`           |
| `mosparoweb.serviceAccount`                              | ``                 |



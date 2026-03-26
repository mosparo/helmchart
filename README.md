# mosparo

A Helm chart for mosparo

This chart was created from the docker-compose.yaml example with the great tool [Katenary](https://github.com/metal3d/katenary) (v3 pre release) and adjusted manually: shared RWX-Volume, network policy

## Adding the Helm Repository

Add the mosparo Helm repository to your local Helm installation:

```bash
helm repo add mosparo https://mosparo.github.io/helmchart
helm repo update
```

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
| `mosparoweb.imagePullPolicy`                             | `Always`           |
| `mosparoweb.ingress.class`                               | `-`                |
| `mosparoweb.ingress.enabled`                             | `true`             |
| `mosparoweb.ingress.host`                                | ``                 |
| `mosparoweb.ingress.path`                                | `/`                |
| `mosparoweb.persistence.mosparodata.accessMode[0].value` | `ReadWriteMany`    |
| `mosparoweb.persistence.mosparodata.enabled`             | `true`             |
| `mosparoweb.persistence.mosparodata.size`                | `1Gi`              |
| `mosparoweb.persistence.mosparodata.storageClass`        | `-`                |
| `mosparoweb.replicas`                                    | `1`                |
| `mosparoweb.repository.image`                            | `mosparo/mosparo`  |
| `mosparoweb.repository.tag`                              | `latest`           |
| `mosparoweb.serviceAccount`                              | ``                 |



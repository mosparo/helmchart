# mosparo

A Helm chart for mosparo

This chart was created from the docker-compose.yaml example with the great tool [Katenary](https://github.com/metal3d/katenary) (v3 pre release) and adjusted manually: shared RWX-Volume, network policy

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
# Standard Helm install
$ helm install  my-release mosparo

# To use a custom namespace and force the creation of the namespace
$ helm install my-release --namespace my-namespace --create-namespace mosparo

# To use a custom values file
$ helm install my-release -f my-values.yaml mosparo
```

See the [Helm documentation](https://helm.sh/docs/intro/using_helm/) for more information on installing and managing the chart.

## Configuration

The following table lists the configurable parameters of the mosparo chart and their default values.

| Parameter                                                 | Default                     |
| --------------------------------------------------------- | --------------------------- |
| `db.environment.MYSQL_PASSWORD`                           | `mosparo_password`          |
| `db.environment.MYSQL_ROOT_PASSWORD`                      | `mosparo_root_pw`           |
| `db.imagePullPolicy`                                      | `IfNotPresent`              |
| `db.persistence.dbdata.accessMode[0].value`               | `ReadWriteOnce`             |
| `db.persistence.dbdata.enabled`                           | `true`                      |
| `db.persistence.dbdata.size`                              | `1Gi`                       |
| `db.persistence.dbdata.storageClass`                      | `-`                         |
| `db.replicas`                                             | `1`                         |
| `db.repository.image`                                     | `mariadb`                   |
| `db.repository.tag`                                       | `10.10`                     |
| `db.serviceAccount`                                       | ``                          |
| `mosparocron.imagePullPolicy`                             | `Always`                    |
| `mosparocron.persistence.mosparodata.enabled`             | `true`                      |
| `mosparocron.replicas`                                    | `1`                         |
| `mosparocron.repository.image`                            | `mosparo/mosparo`           |
| `mosparocron.repository.tag`                              | `latest`                    |
| `mosparocron.serviceAccount`                              | ``                          |
| `mosparoweb.imagePullPolicy`                              | `Always`                    |
| `mosparoweb.ingress.class`                                | `-`                         |
| `mosparoweb.ingress.enabled`                              | `true`                      |
| `mosparoweb.ingress.host`                                 | ``                          |
| `mosparoweb.ingress.path`                                 | `/`                         |
| `mosparoweb.persistence.mosparodata.accessMode[0].value`  | `ReadWriteMany`             |
| `mosparoweb.persistence.mosparodata.enabled`              | `true`                      |
| `mosparoweb.persistence.mosparodata.size`                 | `1Gi`                       |
| `mosparoweb.persistence.mosparodata.storageClass`         | `-`                         |
| `mosparoweb.replicas`                                     | `1`                         |
| `mosparoweb.repository.image`                             | `mosparo/mosparo`           |
| `mosparoweb.repository.tag`                               | `latest`                    |
| `mosparoweb.serviceAccount`                               | ``                          |



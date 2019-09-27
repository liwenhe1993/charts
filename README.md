# ClickHouse

[ClickHouse](https://clickhouse.yandex/) is an open source column-oriented database management system capable of real time generation of analytical data reports using SQL queries.

## Introduction
This chart bootstraps a [ClickHouse](https://clickhouse.yandex/) replication cluster deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.10+
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm repo add liwenhe1993 https://liwenhe1993.github.io/clickhouse-charts/
$ helm repo update
$ helm install --name clickhouse liwenhe1993/clickhouse
```
These commands deploy Clickhouse on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `clickhouse` deployment:

```bash
$ helm delete --purge clickhouse
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following tables lists the configurable parameters of the Clickhouse chart and their default values.

| Parameter                                                                         | Description                                                                                                                    | Default                                               |
| --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------- |
| `timezone`                                                                        | World time and date for cities in all time zones                                                                               | `Asia/Shanghai`                                       |
| `clusterDomain`                                                                   | Kubernetes cluster domain                                                                                                      | `cluster.local`                                       |
| `affinity`                                                                        | Clickhouse Node selectors and tolerations for pod assignment                                                                   | `nil`                                                 |
| `clickhouse.podManagementPolicy`                                                  | StatefulSet controller supports relax its ordering guarantees while preserving its uniqueness and identity guarantees          | `Parallel`                                            |
| `clickhouse.updateStrategy`                                                       | StatefulSet controller supports automated updates. There are two valid update strategies: RollingUpdate and OnDelete           | `RollingUpdate`                                       |
| `clickhouse.rollingUpdatePartition`                                               | Partition update strategy                                                                                                      | `nil`                                                 |
| `clickhouse.path`                                                                 | The path to the directory containing data                                                                                      | `/var/lib/clickhouse`                                 |
| `clickhouse.http_port`                                                            | The port for connecting to the server over HTTP                                                                                | `8123`                                                |
| `clickhouse.tcp_port`                                                             | Port for communicating with clients over the TCP protocol                                                                      | `9000`                                                |
| `clickhouse.interserver_http_port`                                                | Port for exchanging data between ClickHouse servers                                                                            | `9009`                                                |
| `clickhouse.replicas`                                                             | The instance number of Clickhouse                                                                                              | `3`                                                   |
| `clickhouse.image`                                                                | Docker image for Clickhouse                                                                                                    | `yandex/clickhouse-server`                            |
| `clickhouse.imageVersion`                                                         | Docker image version for Clickhouse                                                                                            | `19.14`                                               |
| `clickhouse.imagePullPolicy`                                                      | Image pull policy. One of Always, Never, IfNotPresent                                                                          | `IfNotPresent`                                        |
| `clickhouse.livenessProbe.enabled`                                                | Turn on and off liveness probe                                                                                                 | `true`                                                |
| `clickhouse.livenessProbe.initialDelaySeconds`                                    | Delay before liveness probe is initiated                                                                                       | `30`                                                  |
| `clickhouse.livenessProbe.periodSeconds`                                          | How often to perform the probe                                                                                                 | `30`                                                  |
| `clickhouse.livenessProbe.timeoutSeconds`                                         | When the probe times out                                                                                                       | `5`                                                   |
| `clickhouse.livenessProbe.failureThreshold`                                       | Minimum consecutive successes for the probe                                                                                    | `3`                                                   |
| `clickhouse.livenessProbe.successThreshold`                                       | Minimum consecutive failures for the probe                                                                                     | `1`                                                   |
| `clickhouse.readinessProbe.enabled`                                               | Turn on and off readiness probe                                                                                                | `true`                                                |
| `clickhouse.readinessProbe.initialDelaySeconds`                                   | Delay before readiness probe is initiated                                                                                      | `30`                                                  |
| `clickhouse.readinessProbe.periodSeconds`                                         | How often to perform the probe                                                                                                 | `30`                                                  |
| `clickhouse.readinessProbe.timeoutSeconds`                                        | When the probe times out                                                                                                       | `5`                                                   |
| `clickhouse.readinessProbe.failureThreshold`                                      | Minimum consecutive successes for the probe                                                                                    | `3`                                                   |
| `clickhouse.readinessProbe.successThreshold`                                      | Minimum consecutive failures for the probe                                                                                     | `1`                                                   |
| `clickhouse.persistentVolumeClaim.enabled`                                        | Enable persistence using a `PersistentVolumeClaim`                                                                             | `false`                                               |
| `clickhouse.persistentVolumeClaim.dataPersistentVolume.enabled`                   | Turn on and off dataPersistentVolume                                                                                           | `false`                                               |          
| `clickhouse.persistentVolumeClaim.dataPersistentVolume.accessModes`               | Persistent Volume Access Modes                                                                                                 | `[ReadWriteOnce]`                                     |                  
| `clickhouse.persistentVolumeClaim.dataPersistentVolume.storageClassName`          | Persistent Volume Storage Class                                                                                                | ``                                                    |                  
| `clickhouse.persistentVolumeClaim.dataPersistentVolume.storage`                   | Persistent Volume Size                                                                                                         | `500Gi`                                               |                  
| `clickhouse.persistentVolumeClaim.logsPersistentVolume.enabled`                   | Turn on and off dataPersistentVolume                                                                                           | `false`                                               |          
| `clickhouse.persistentVolumeClaim.logsPersistentVolume.accessModes`               | Persistent Volume Access Modes                                                                                                 | `[ReadWriteOnce]`                                     |                  
| `clickhouse.persistentVolumeClaim.logsPersistentVolume.storageClassName`          | Persistent Volume Storage Class                                                                                                | ``                                                    |                  
| `clickhouse.persistentVolumeClaim.logsPersistentVolume.storage`                   | Persistent Volume Size                                                                                                         | `50Gi`                                                |                  
| `clickhouse.ingress.enabled`                                                      | Enable ingress                                                                                                                 | `false`                                               |
| `clickhouse.ingress.host`                                                         | Ingress host                                                                                                                   | ``                                                    |
| `clickhouse.ingress.path`                                                         | Ingress path                                                                                                                   | ``                                                    |
| `clickhouse.ingress.tls.enabled`                                                  | Enable ingress tls                                                                                                             | `false`                                               |
| `clickhouse.ingress.tls.hosts`                                                    | Ingress tls hosts                                                                                                              | `[]`                                                  |
| `clickhouse.ingress.tls.secretName`                                               | Ingress tls `secretName`                                                                                                       | ``                                                    |
| `clickhouse.configmap.enabled`                                                    | If Configmap's enabled is `true`, Custom `config.xml`, `metrica.xml` and `users.xml`                                           | `true`                                                |
| `clickhouse.configmap.max_connections`                                            | The maximum number of inbound connections                                                                                      | `4096`                                                |
| `clickhouse.configmap.keep_alive_timeout`                                         | The number of seconds that ClickHouse waits for incoming requests before closing the connection                                | `3`                                                   |
| `clickhouse.configmap.max_concurrent_queries`                                     | The maximum number of simultaneously processed requests                                                                        | `100`                                                 |
| `clickhouse.configmap.uncompressed_cache_size`                                    | Cache size (in bytes) for uncompressed data used by table engines from the MergeTree                                           | `8589934592`                                          |
| `clickhouse.configmap.mark_cache_size`                                            | Approximate size (in bytes) of the cache of "marks" used by MergeTree                                                          | `5368709120`                                          |
| `clickhouse.configmap.umask`                                                      | Number is always parsed as octal. Default umask is 027 (other users cannot read logs, data files, etc; group can only read)    | `022`                                                 |
| `clickhouse.configmap.mlock_executable`                                           | Enabling this option is recommended but will lead to increased startup time for up to a few seconds                            | `false`                                               |
| `clickhouse.configmap.builtin_dictionaries_reload_interval`                       | The interval in seconds before reloading built-in dictionaries                                                                 | `3600`                                                |
| `clickhouse.configmap.max_session_timeout`                                        | Maximum session timeout, in seconds                                                                                            | `3600`                                                |
| `clickhouse.configmap.default_session_timeout`                                    | Default session timeout, in seconds                                                                                            | `60`                                                  |
| `clickhouse.configmap.disable_internal_dns_cache`                                 | Uncomment to disable ClickHouse internal DNS caching                                                                           | `1`                                                   |
| `clickhouse.configmap.max_open_files`                                             | The maximum number of open files                                                                                               | ``                                                    |
| `clickhouse.configmap.interserver_http_host`                                      | The host name that can be used by other servers to access this server                                                          | ``                                                    |
| `clickhouse.configmap.logger.path`                                                | The log file path                                                                                                              | `/var/log/clickhouse-server`                          |
| `clickhouse.configmap.logger.level`                                               | Logging level. Acceptable values: trace, debug, information, warning, error                                                    | `trace`                                               |
| `clickhouse.configmap.logger.size`                                                | Size of the file                                                                                                               | `1000M`                                               |
| `clickhouse.configmap.logger.count`                                               | The number of archived log files that ClickHouse stores                                                                        | `10`                                                  |
| `clickhouse.configmap.compression.enabled`                                        | Enable data compression settings                                                                                               | `false`                                               |
| `clickhouse.configmap.compression.cases[].min_part_size`                          | The minimum size of a table part                                                                                               | `10000000000`                                         |
| `clickhouse.configmap.compression.cases[].min_part_size_ratio`                    | The ratio of the minimum size of a table part to the full size of the table                                                    | `0.01`                                                |
| `clickhouse.configmap.compression.cases[].method`                                 | Compression method. Acceptable values ​: lz4 or zstd(experimental)                                                              | `zstd`                                                |
| `clickhouse.configmap.zookeeper_servers.enabled`                                  | Enable contains settings that allow ClickHouse to interact with a ZooKeeper cluster                                            | `false`                                               |
| `clickhouse.configmap.zookeeper_servers.session_timeout_ms`                       | Maximum timeout for the client session in milliseconds                                                                         | `30000`                                               |
| `clickhouse.configmap.zookeeper_servers.operation_timeout_ms`                     | Operation timeout for the client session in milliseconds                                                                       | `10000`                                               |
| `clickhouse.configmap.zookeeper_servers.root`                                     | The znode that is used as the root for znodes used by the ClickHouse server. Optional                                          | ``                                                    |
| `clickhouse.configmap.zookeeper_servers.identity`                                 | User and password, that can be required by ZooKeeper to give access to requested znodes. Optional                              | ``                                                    |
| `clickhouse.configmap.zookeeper_servers.config[].index`                           | ZooKeeper index                                                                                                                | ``                                                    |
| `clickhouse.configmap.zookeeper_servers.config[].host`                            | ZooKeeper host                                                                                                                 | ``                                                    |
| `clickhouse.configmap.zookeeper_servers.config[].port`                            | ZooKeeper port                                                                                                                 | ``                                                    |
| `clickhouse.configmap.remote_servers.enabled`                                     | Enable configuration of clusters used by the Distributed table engine                                                          | `true`                                                |
| `clickhouse.configmap.remote_servers.internal_replication`                        | If this parameter is set to 'true', the table where data will be written is going to replicate them itself                     | `false`                                               |
| `clickhouse.configmap.remote_servers.replica.user`                                | Name of the user for connecting to a remote server. Access is configured in the users.xml file.                                | `default`                                             |
| `clickhouse.configmap.remote_servers.replica.password`                            | The password for connecting to a remote server (not masked).                                                                   | `default`                                             |
| `clickhouse.configmap.remote_servers.replica.compression`                         | Use data compression.                                                                                                          | `true`                                                |
| `clickhouse.configmap.remote_servers.replica.backup.enabled`                      | Enable replica backup                                                                                                          | `false`                                               |
| `clickhouse.configmap.remote_servers.graphite.enabled`                            | Enable graphite                                                                                                                | `false`                                               |
| `clickhouse.configmap.remote_servers.graphite.config[].timeout`                   | The timeout for sending data, in seconds                                                                                       | `0.1`                                                 |
| `clickhouse.configmap.remote_servers.graphite.config[].interval`                  | The interval for sending, in seconds                                                                                           | `60`                                                  |
| `clickhouse.configmap.remote_servers.graphite.config[].root_path`                 | Prefix for keys                                                                                                                | `one_min`                                             |
| `clickhouse.configmap.remote_servers.graphite.config[].metrics`                   | Sending data from a :ref:system_tables-system.metrics table                                                                    | `true`                                                |
| `clickhouse.configmap.remote_servers.graphite.config[].events`                    | Sending deltas data accumulated for the time period from a :ref:system_tables-system.events table                              | `true`                                                |
| `clickhouse.configmap.remote_servers.graphite.config[].events_cumulative`         | Sending cumulative data from a :ref:system_tables-system.events table                                                          | `true`                                                |
| `clickhouse.configmap.remote_servers.graphite.config[].asynchronous_metrics`      | Sending data from a :ref:system_tables-system.asynchronous_metrics table                                                       | `true`                                                |
| `clickhouse.configmap.remote_servers.profiles.enabled`                            | Enable a settings profiles                                                                                                     | `false`                                               |
| `clickhouse.configmap.remote_servers.profiles.profile[].name`                     | Tne name of a settings profile                                                                                                 | ``                                                    |
| `clickhouse.configmap.remote_servers.profiles.profile[].config`                   | The config of a settings profile                                                                                               | `{}`                                                  |
| `clickhouse.configmap.remote_servers.profiles.users.enabled`                      | Enable a settings users                                                                                                        | `false`                                               |
| `clickhouse.configmap.remote_servers.profiles.users[].name`                       | Tne name of a settings user                                                                                                    | ``                                                    |
| `clickhouse.configmap.remote_servers.profiles.users[].config`                     | Tne config of a settings user                                                                                                  | `{}`                                                  |
| `clickhouse.configmap.remote_servers.profiles.quotas.enabled`                     | Enable a settings quotas                                                                                                       | `false`                                               |
| `clickhouse.configmap.remote_servers.profiles.quotas[].name`                      | Tne name of a settings quota                                                                                                   | ``                                                    |
| `clickhouse.configmap.remote_servers.profiles.quotas[].config`                    | Tne config of a settings quota                                                                                                 | `{}`                                                  |
| `tabix.enabled`                                                                   | Enable tabix                                                                                                                   | `false`                                               |
| `tabix.replicas`                                                                  | The instance number of Tabix                                                                                                   | `1`                                                   |
| `tabix.updateStrategy.type`                                                       | Type of deployment. Can be "Recreate" or "RollingUpdate". Default is RollingUpdate                                             | `RollingUpdate`                                       |
| `tabix.updateStrategy.maxSurge`                                                   | The maximum number of pods that can be scheduled above the desired number of pods                                              | `3`                                                   |
| `tabix.updateStrategy.maxUnavailable`                                             | The maximum number of pods that can be unavailable during the update                                                           | `1`                                                   |
| `tabix.image`                                                                     | Docker image name                                                                                                              | `spoonest/clickhouse-tabix-web-client`                |
| `tabix.imageVersion`                                                              | Docker image version                                                                                                           | `stable`                                              |
| `tabix.imagePullPolicy`                                                           | Dcoker image pull policy                                                                                                       | `IfNotPresent`                                        |
| `tabix.livenessProbe.enabled`                                                     | Turn on and off liveness probe                                                                                                 | `true`                                                |
| `tabix.livenessProbe.initialDelaySeconds`                                         | Delay before liveness probe is initiated                                                                                       | `30`                                                  |
| `tabix.livenessProbe.periodSeconds`                                               | How often to perform the probe                                                                                                 | `30`                                                  |
| `tabix.livenessProbe.timeoutSeconds`                                              | When the probe times out                                                                                                       | `5`                                                   |
| `tabix.livenessProbe.failureThreshold`                                            | Minimum consecutive successes for the probe                                                                                    | `3`                                                   |
| `tabix.livenessProbe.successThreshold`                                            | Minimum consecutive failures for the probe                                                                                     | `1`                                                   |
| `tabix.readinessProbe.enabled`                                                    | Turn on and off readiness probe                                                                                                | `true`                                                |
| `tabix.readinessProbe.initialDelaySeconds`                                        | Delay before readiness probe is initiated                                                                                      | `30`                                                  |
| `tabix.readinessProbe.periodSeconds`                                              | How often to perform the probe                                                                                                 | `30`                                                  |
| `tabix.readinessProbe.timeoutSeconds`                                             | When the probe times out                                                                                                       | `5`                                                   |
| `tabix.readinessProbe.failureThreshold`                                           | Minimum consecutive successes for the probe                                                                                    | `3`                                                   |
| `tabix.readinessProbe.successThreshold`                                           | Minimum consecutive failures for the probe                                                                                     | `1`                                                   |
| `tabix.security.user`                                                             | Tabix login username                                                                                                           | `admin`                                               |
| `tabix.security.password`                                                         | Tabix login password                                                                                                           | `admin`                                               |
| `tabix.automaticConnection.chName`                                                | Automatic connection Clickhouse name                                                                                           | ``                                                    |
| `tabix.automaticConnection.chHost`                                                | Automatic connection Clickhouse host                                                                                           | ``                                                    |
| `tabix.automaticConnection.chLogin`                                               | Automatic connection Clickhouse login username                                                                                 | ``                                                    |
| `tabix.automaticConnection.chPassword`                                            | Automatic connection Clickhouse login password                                                                                 | ``                                                    |
| `tabix.automaticConnection.chParams`                                              | Automatic connection Clickhouse params                                                                                         | ``                                                    |
| `tabix.ingress.enabled`                                                           | Enable ingress                                                                                                                 | `false`                                               |
| `tabix.ingress.host`                                                              | Ingress host                                                                                                                   | ``                                                    |
| `tabix.ingress.path`                                                              | Ingress path                                                                                                                   | ``                                                    |
| `tabix.ingress.tls.enabled`                                                       | Enable ingress tls                                                                                                             | `false`                                               |
| `tabix.ingress.tls.hosts`                                                         | Ingress tls hosts                                                                                                              | `[]`                                                  |

For more information please refer to the [liwenhe/clickhouse-charts](https://github.com/liwenhe1993/clickhouse-charts.git) documentation.

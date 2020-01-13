# Azure Devops Agent

## Prerequisites

- Kubernetes 1.11+
- Helm 3

## Installing the Chart

To install the chart with the release name `my-release` in namespace `my-namespace`:

```console
$ helm upgrade --install --namespace my-namespace my-release -f values.yaml .
```

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

The following table lists the configurable parameters of the WordPress chart and their default values.

|            Parameter                       |                                  Description                                 |                           Default                            |
| ------------------------------------------ | ---------------------------------------------------------------------------- | ------------------------------------------------------------ |
| `image.registry`                           | Zabbix server mysql image registry                                           | `docker.io`                                                  |
| `image.repository`                         | Zabbix server image name                                                     | `zabbix/zabbix-server-mysql`                                 |
| `image.tag`                                | Zabbix server image tag                                                      | `{TAG_NAME}`                                                 |
| `image.pullPolicy`                         | Image pull policy                                                            | `IfNotPresent`                                               |
| `image.pullSecrets`                        | Specify docker-registry secret names as an array                             | `[]` (does not add image pull secrets to deployed pods)      |
| `nameOverride.`                            | Strings to partially override fullname templates with a string (will prepend the release name) | `nil`                                      |
| `fullnameOverride.`                        | Strings to fully override fullname templates with a string                                     | `nil`                                      |
| `replicaCount`                             | Number of Web Pods to run                                                    | `2`                                                          |
| `schedulerName`                           | Name of the alternate scheduler                                               | `nil`                                                        |
| `nodeSelector`                            | Node labels for pod assignment                                                | `{}`                                                         |
| `tolerations`                             | List of node taints to tolerate                                               | `[]`                                                         |
| `affinity`                                | Map of node/pod affinities                                                    | `{}`                                                         |
| `podAnnotations`                          | Pod annotations                                                               | `{}`                                                         |
| `updateStrategy`                          | Set up update strategy                                                        | `RollingUpdate` for web and `Recreate` for server            |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
$ helm install --name my-release \
  --set azp.token=aksjdfjkhadfsjkhkjsdgfjkhagsdf \
    .
```

The above command sets the visible Zabbix installation name in right top corner of the web interface.

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
$ helm install --name my-release -f values.yaml .
```

> **Tip**: You can use the default [values.yaml](values.yaml) but you need to specify azp.url and azp.token to connect the agent to some Azure Devops service


## Configuration and installation details

### Production configuration

- Number of Agents
```diff
- replicaCount: 1
+ replicaCount: 2
```
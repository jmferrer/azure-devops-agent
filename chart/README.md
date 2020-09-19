# Azure Pipelines Agent

## Prerequisites

- Kubernetes 1.11+
- Helm 3

## Installing the Chart

To install the chart with the release name `my-release` in namespace `my-namespace`:

```console
$ helm repo add fermosit https://harbor.fermosit.es/chartrepo/library
$ helm upgrade --install --namespace my-namespace my-release
    --set azp.token=aksjdfjkhadfsjkhkjsdgfjkhagsdf \
    --set azp.url=https://dev.azure.com/yourazuregroup \
    fermosit/.
```

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

The following table lists the configurable parameters of the Azure Pipelines Agent chart and their default values.

|       Parameter     |                                  Description                                                       |                           Default                            |
| --------------------| -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| `azp.url`           | Azure Pipelines group                                                                              | `https://dev.azure.com/yourazuregroup` (mandatory)           | 
| `azp.token`         | Azure Pipelines token                                                                              | `myverysecuretoken` (mandatory                               |
| `azp.agent_name`    | Azure Pipelines agent name                                                                         | `latest`                                                     |
| `azp.pool`          | Azure Pipelines pool                                                                               | `Default`                                                    |
| `azp.work`          | Azure Pipelines work directory (workspace used by agent)                                           | `_work`                                                      |
| `secrets`           | List of secrets that will be environment vars in the running azure pipelines agent pod             | `[]`                                                         |
| `image.registry`    | Image registry                                                                                     | `docker.io`                                                  |
| `image.repository`  | Image name                                                                                         | `jmferrer/azure-devops-agent`                                |
| `image.tag`         | Image tag                                                                                          | `latest`                                                     |
| `image.pullPolicy`  | Image pull policy                                                                                  | `Always`                                                     |
| `image.pullSecrets` | Image pull secret name                                                                             | `[]`                                                         |
| `nameOverride`      | String to partially override azure-devops-agent.fullname template (will maintain the release name) | `null`                                                       |
| `fullnameOverride`  | String to fully override azure-devops-agent.fullname template                                      | `null`                                                       |
| `replicaCount`      | Number of agents in statefulset                                                                    | `1`                                                          |
| `resources`         | Configure resource requests and limits                                                             | `{}`                                                         |
| `http_proxy`        | HTTP proxy endpoint to use for containers                                                          | `null`                                                       |
| `https_proxy`       | HTTPS proxy endpoint to use for containers                                                         | `null`                                                       |
| `no_proxy`          | Blacklist of addresses to skip the proxy when reaching                                             | `null`                                                       |
| `nodeSelector`      | Node labels for pod assignment                                                                     | `{}`                                                         |
| `tolerations`       | Tolerations for pod assignment                                                                     | `[]`                                                         |
| `affinity`          | Affinity for pod assignment                                                                        | `{}`                                                         |
| `podAnnotations`    | Pod annotations                                                                                    | `{}`                                                         |
| `sidecars`          | Add sidecars to the pod                                                                            | `null`

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
$ helm install --name my-release \
    --set azp.token=aksjdfjkhadfsjkhkjsdgfjkhagsdf \
    --set azp.url=https://dev.azure.com/yourazuregroup \
    .
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
$ helm install --name my-release -f values.yaml .
```

> **Tip**: You can use the default [values.yaml](values.yaml) but you need to specify azp.url and azp.token to connect the agent to some Azure Devops service


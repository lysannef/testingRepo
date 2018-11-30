# Mesos

[Mesos](http://mesos.apache.org/)Apache Mesos abstracts CPU, memory, storage, and other compute resources away from machines (physical or virtual), enabling fault-tolerant and elastic distributed systems to easily be built and run effectively.

```console
$ helm install stable/ibm-mesos
```

## Prerequisites

- Kubernetes 1.7+ 
- Tiller 2.7.2 or later

## Resources Required
The chart deploys pods consuming minimum resources as specified in the resources configuration parameter (default: Memory: 200Mi, CPU: 100m)

## Introduction

This chart bootstraps a [Mesos](https://github.com/apache/mesos) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.


## Installing the Chart

To install the chart with the release name `my-release`:

```console
$ helm intall --name my-release stable/ibm-mesos
```

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Chart Details
This chart bootstraps a [Mesos](https://hub.docker.com/r/ibmcom/mesos-ppc64le/) deployment on a [Kubernetes](http://kubernetes.io) cluster


## Configuration

The following table lists the configurable parameters of the Mesos chart and their default values.

|      Parameter            |          Description            |                         Default                         |
|---------------------------|---------------------------------|---------------------------------------------------------|
| `image`                   | The image to pull and run       | default ex. ibmcom/mesos-ppc64le:1.1.0                  |
| `imagePullPolicy`         | Image pull policy               | `Always` if `imageTag` is `latest`, else `IfNotPresent` |
| `nodeSelector`            | Specify what architecture Node  |             `ppc64le`                                    |


The above parameters map to `ibm-mesos` params.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. 

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml stable/ibm-mesos
```

> **Tip**: You can use the default `values.yaml`

### Persistence

If `persistence` is enabled, PVC's will be used to store the web root and the db root. If a pod then is redeployed to another node, it will restart within seconds with the old state prevailing. If it is disabled, `EmptyDir` is used, which would lead to deletion of the persistent storage once the pod is moved. Also cloning a chart with `persistence` disabled will not work. Therefor persistence is enabled by default and should only be disabled in a testing environment. In environments where no PVCs are available you can use `persistence.hostPath` instead. This will store the charts persistent data on the node it is running on.

| Parameter | Description | Default |
| - | - | - |
| `persistence.enabled` | Enables persistent volume - PV provisioner support necessary | true |
| `persistence.keep` | Keep persistent volume after helm delete | false |
| `persistence.accessMode` | PVC Access Mode | ReadWriteOnce |
| `persistence.size` | PVC Size | 2Gi |
| `persistence.storageClass` | PVC Storage Class | _empty_ |
| `persistence.hostPath` | if specified, used as persistent storage instead of PVC | _empty_ |

## Limitations

## NOTE
This chart has been validated on ppc64le.

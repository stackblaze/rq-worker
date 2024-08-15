

# RQ Worker Helm Chart

## Introduction

This Helm chart deploys RQ (Redis Queue) workers on a Kubernetes cluster. RQ is a simple Python library for queueing jobs and processing them in the background with workers. This chart makes it easy to deploy and manage RQ workers in a Kubernetes environment.

## Prerequisites

- Kubernetes 1.12+
- Helm 3.0+
- Redis instance (can be deployed separately or as a dependency)

## Repository

The source code for this chart is available at:
[https://github.com/stackblaze/rq-worker.git](https://github.com/stackblaze/rq-worker.git)

Configuration
-------------

The following table lists the configurable parameters of the rq-worker chart and their default values.

| Parameter | Description | Default |
| --- | --- | --- |
| `replicaCount` | Number of RQ worker replicas | `1` |
| `image.repository` | RQ worker image repository | `stackblaze/rq-worker` |
| `image.tag` | RQ worker image tag | `latest` |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |
| `redis.host` | Redis host | `redis-service` |
| `redis.port` | Redis port | `6379` |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example:


`helm install my-rq-worker stackblaze/rq-worker --set replicaCount=3  `

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example:


`helm install my-rq-worker stackblaze/rq-worker -f values.yaml `

Usage
-----

Scaling Workers
---------------

To scale the number of worker replicas:

`kubectl scale deployment my-rq-worker --replicas=5  `

Viewing Logs
------------

To view the logs of a worker:

`kubectl logs -l app=rq-worker `

Monitoring
----------

You can use Kubernetes native tools like `kubectl` to monitor the status of your workers:

`kubectl get pods -l app=rq-worker `

Uninstalling the Chart
----------------------

To uninstall/delete the `my-rq-worker` deployment:

`helm delete my-rq-worker `

Contributing
------------

We welcome contributions to this chart. Please read our [Contributing Guide](https://www.perplexity.ai/search/CONTRIBUTING.md) for more information on how to get started.

License
-------

This chart is licensed under the MIT License. See the [LICENSE](https://www.perplexity.ai/search/LICENSE) file for details.

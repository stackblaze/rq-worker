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

## Installation

To install the RQ Worker chart, add the Stackblaze Helm repository and update it:

```bash

helm repo add stackblaze https://stackblaze.github.io/rq-worker

helm repo update

```

Then, install the chart using:

```bash

helm install rq-worker stackblaze/rq-worker -n stackblaze-prod -f values-secret.yaml

```

## Configuration

The following table lists the configurable parameters of the rq-worker chart and their default values.

| Parameter           | Description                  | Default                  |

|---------------------|------------------------------|--------------------------|

| `replicaCount`      | Number of RQ worker replicas | `1`                      |

| `image.repository`  | RQ worker image repository   | `stackblaze/rq-worker`   |

| `image.tag`         | RQ worker image tag          | `latest`                 |

| `image.pullPolicy`  | Image pull policy            | `IfNotPresent`           |

| `redis.host`        | Redis host                   | `redis-service`          |

| `redis.port`        | Redis port                   | `6379`                   |

### Values Example with Referencing a Secret

```yaml

kubernetesClusterDomain: cluster.local

rqWorker:

  replicas: 1

  worker:

    env:

      redisHost: redis-master

      redisPort: "6379"

      redisUsername: "default"  # Provide the username directly

      redisPasswordSecret:

        name: redis

        key: redis-password

    image:

      repository: stackblaze/rq-worker

      tag: latest

```

### Values Example without a Secret

```yaml

rqWorker:

  replicas: 1

  worker:

    env:

      redisHost: redis-master

      redisPort: "6379"

      redisUsername: "default"

      redisPassword: "E9vxtfeLBy"

    image:

      repository: stackblaze/rq-worker

      tag: latest

```

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example:

```bash

helm install my-rq-worker stackblaze/rq-worker --set replicaCount=3

```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example:

```bash

helm install my-rq-worker stackblaze/rq-worker -f values.yaml

```

## Usage

### Scaling Workers

To scale the number of worker replicas:

```bash

kubectl scale deployment my-rq-worker --replicas=5

```

### Viewing Logs

To view the logs of a worker:

```bash

kubectl logs -l app=rq-worker

```

### Monitoring

You can use Kubernetes native tools like `kubectl` to monitor the status of your workers:

```bash

kubectl get pods -l app=rq-worker

```

### Uninstalling the Chart

To uninstall/delete the `my-rq-worker` deployment:

```bash

helm delete my-rq-worker

```

## Contributing

We welcome contributions to this chart. Please read our [Contributing Guide](https://github.com/stackblaze/rq-worker/blob/main/CONTRIBUTING.md) for more information on how to get started.

## License

This chart is licensed under the MIT License. See the [LICENSE](https://github.com/stackblaze/rq-worker/blob/main/LICENSE) file for details.

---

This updated README includes installation instructions, examples of values with and without using a secret, and removes outdated documentation. Adjust the links to the `CONTRIBUTING.md` and `LICENSE` files as needed, based on your repository structure.
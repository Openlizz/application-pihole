<h1 align="center">Lizz compatible Pi-hole application</h1>

Lizz compatible application to add the [Pi-hole application](https://pi-hole.net/) to a Lizz managed Kubernetes cluster.

To learn more about Lizz, see the [documentation](https://openlizz.com).

## Requirements

To add the application, you first need to have a [Kubernetes cluster initialized with Lizz](https://openlizz.com/docs/guides/init).
You also need to have the [Lizz CLI installed](https://openlizz.com/docs/installation).

## Add the application

To add the application to your cluster, run the following:

```bash
lizz add github \
    --owner=$GITHUB_USER  \
    --fleet=fleet \
    --origin-url=https://github.com/openlizz/application-pihole \
    --path=./default \
    --destination=pihole \
    --set-value loadBalancerIp=192.168.1.245
    --personal
```

Check the [guide](https://openlizz.com/docs/guides/add) to understand how works the lizz add command.

> **Note**
> You can adapt the command depending on your use case. See the [command API](https://openlizz.com/docs/cli/lizz_add_github) for more information.

Reconcile the fleet repository to deploy the application using [Flux](https://fluxcd.io/):

```
flux reconcile source git flux-system
```

Check the pods with:

```
kubectl get pod -n pihole
```

The output should be similar to:

```
NAMESPACE       NAME                                        READY   STATUS    RESTARTS      AGE
```

## Usage

Access the application using port-forwarding or using the ingress created.

## Acknowledgements

This repository is only a wrapper to the [Helm chart](https://github.com/MoJo2600/pihole-kubernetes/tree/master/charts/pihole) of the [Pi-hole application](https://pi-hole.net/) to help its deployment in a Kubernetes cluster managed by Lizz.

Therefore, the credit goes to the developers and maintainers of the application and the chart.

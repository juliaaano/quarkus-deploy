# Quarkus Deploy

Deploys the project [https://github.com/juliaaano/quarkus](https://github.com/juliaaano/quarkus) on Kubernetes or OpenShift.

This project is meant to be watched by ArgoCD.

See details below for instructions and requirements.

```
$ helm install myrelease -f values-dev.yaml chart
```

## Sealed Secrets

From [https://github.com/bitnami-labs/sealed-secrets](https://github.com/bitnami-labs/sealed-secrets):

### Cluster Installation

Requires cluster admin access.

```
$ kubectl apply -f https://github.com/bitnami-labs/sealed-secrets/releases/download/v0.16.0/controller.yaml
```

### CLI Installation

Depends on the client's environment.

```
$ brew install kubeseal
```

### Verify

Check if controller is up by retrieving the public key.

```
$ kubeseal --fetch-cert --controller-name=sealed-secrets-controller --controller-namespace=kube-system
```

### Create RAW Sealed Secret

Set raw encrypted secret as a Helm value. Keep '--name' as it is.

```
$ echo -n username | kubeseal --raw --from-file=/dev/stdin --scope cluster-wide
$ echo -n password | kubeseal --raw --from-file=/dev/stdin --scope cluster-wide
```

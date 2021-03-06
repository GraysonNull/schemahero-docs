---
date: 2019-10-09
linktitle: "Installing SchemaHero"
title: Installing SchemaHero
weight: 2
aliases:
  - /docs/installing
---


SchemaHero has 2 different components: an in-cluster Kubernetes Operator and a client side kubectl plugin that you can use to interact with the operator. The best way to get started, is to install the kubectl plugin:

## Client

The SchemaHero client-side component is a kubectl plugin that's packaged and delivered using [Krew](https://krew.dev), the package manager for kubectl plugins.

### Install Krew and the SchemaHero plugin at once:
```shell
curl https://krew.sh/schemahero | bash
```

### Install Krew and the SchemaHero plugin as separate steps:
First, install [krew](https://krew.dev), by following the [documented installation instructions](https://github.com/kubernetes-sigs/krew/#installation).

Once you have the krew package manager installed, you can install the SchemaHero plugin:

```shell
kubectl krew install schemahero
```

## Operator

SchemaHero relies on an in-cluster operator. The next step in the installation is to operator components:

### One Command Deploy

It's easy to install the operator using the built-in command:

```shell
kubectl schemahero install
```

The above command will create a `schemahero-system` namespace, and install 2 new Custom Resource Definitions to your cluster.

### GitOps and Other Workflows

An alternative approach is to let the kubectl plugin generate the YAML that can be checked in, commited and deployed using another tool:

```shell
kubectl schemahero install --yaml
```

This will create the necessary YAML to install the in-cluster SchemaHero operator. After inspection, you can use `kubectl` to `apply` this YAML to you cluster.

## Verification

To verify the deployment, you can run:

```shell
kubectl get pods -n schemahero-system
```

There should be 1 pod running in this namespace:

```shell
$ kubectl get pods -n schemahero-system
NAME           READY   STATUS    RESTARTS   AGE
schemahero-0   1/1     Running   0          66s
```

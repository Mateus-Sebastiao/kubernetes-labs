# Kubernetes Building Blocks

## Nodes

[Nodes](https://kubernetes.io/docs/concepts/architecture/nodes/)

## Namespaces

[Namespaces](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

```bash
$ kubectl get namespaces
$ kubectl create namespace <new-namespace-name>
```

## Pods

[Pods](https://kubernetes.io/docs/concepts/workloads/pods/)

Posso criar o manifest em yaml ou posso gerar com opções simples.

1. Criado:

- [def-pod.yaml](./pods/def-pod.yaml)

2. Criado com a linha de comando:

- [nginx-pod.yaml](./pods/nginx-pod.yaml)

```bash
$ kubectl run nginx-pod --image=nginx:latest --port=80 \
--dry-run=client -o yaml > nginx-pod.yaml
```

Em `json`:

```bash
$ ubectl run nginx-pod --image=nginx:latest --port=80 \
--dry-run=client -o json > nginx-pod.json
```

### Rodar o manifest

```bash
$ kubectl create -f def-pod.yaml
$ kubectl create -f nginx-pod.yaml
```

Forma avançada:

```bash
$ kubectl apply -f nginx-pod.yaml
$ kubectl get pods
$ kubectl get pod nginx-pod -o yaml
$ kubectl get pod nginx-pod -o json
$ kubectl describe pod nginx-pod
$ kubectl delete pod nginx-pod
```

## Labels

[Labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

```bash
$ kubectl get pods --show-labels
$ kubectl get pods -l <dev=label>
```
## Label Selectors

[Label Selectors](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#label-selectors)

## ReplicationController

[Replication Controller](https://kubernetes.io/docs/concepts/workloads/controllers/replicationcontroller/)

## ReplicaSets

[ReplicaSets](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)

[Manifest pronto](./replicaSets/redis-rs.yaml)

```bash
$ kubectl apply -f redis-rs.yaml
$ kubectl get replicasets
$ kubectl get rs
$ kubectl scale rs frontend --replicas=4
$ kubectl get rs frontend -o yaml
$ kubectl get rs frontend -o json
$ kubectl describe rs frontend
$ kubectl delete rs frontend
```
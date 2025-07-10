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
$ kubectl run nginx-pod --image=nginx:latest --port=80 \
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

## Deployments

[Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

Manifest criados:

1. [Manifest_1](./deployments/def-deploy.yaml)

2. [Manifest_2](./deployments/nginx-deploy.yaml)

Comandos:

Em `yaml`:

```bash
kubectl create deployment nginx-deployment \
--image=nginx:1.20.2 --port=80 --replicas=3 \
--dry-run=client -o yaml > nginx-deploy.yaml
```

Em `json`:

```bash
kubectl create deployment nginx-deployment \
--image=nginx:1.20.2 --port=80 --replicas=3 \
--dry-run=client -o json > nginx-deploy.json
```

### Rodar o manifest

```bash
$ kubectl create -f def-deploy.yaml
$ kubectl create -f nginx-deploy.yaml
```

Forma avançada:

```bash
$ kubectl apply -f nginx-deploy.yaml --record
# O --record está descontinuado, nova atualização:
# kubectl annotate deployment nginx-deployment \
#  kubernetes.io/change-cause="Atualizei a imagem para nginx:1.22"
$ kubectl get deployments
$ kubectl get deploy -o wide
$ kubectl scale deploy nginx-deployment --replicas=4
$ kubectl get deploy nginx-deployment -o yaml
$ kubectl get deploy nginx-deployment -o json
$ kubectl describe deploy nginx-deployment
$ kubectl rollout status deploy nginx-deployment
$ kubectl rollout history deploy nginx-deployment
$ kubectl rollout history deploy nginx-deployment --revision=1
$ kubectl set image deploy nginx-deployment nginx=nginx:1.21.5 --record
$ kubectl rollout history deploy nginx-deployment --revision=2
$ kubectl rollout undo deploy nginx-deployment --to-revision=1
$ kubectl get all -l app=nginx-deployment -o wide
$ kubectl delete deploy nginx-deployment
$ kubectl get deploy,rs,po -l app=nginx-deployment
```

## DamonSets

[DamonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)

[Manifest](./damonsets/fluentd-ds.yaml)

```bash
$ kubectl apply -f fluentd-ds.yaml --record
$ kubectl get daemonsets
$ kubectl get ds -o wide
$ kubectl get ds fluentd-agent -o yaml
$ kubectl get ds fluentd-agent -o json
$ kubectl describe ds fluentd-agent
$ kubectl rollout status ds fluentd-agent
$ kubectl rollout history ds fluentd-agent
$ kubectl rollout history ds fluentd-agent --revision=1
$ kubectl set image ds fluentd-agent fluentd=quay.io/fluentd_elasticsearch/fluentd:v4.6.2 --record
$ kubectl rollout history ds fluentd-agent --revision=2
$ kubectl rollout undo ds fluentd-agent --to-revision=1
$ kubectl get all -l k8s-app=fluentd-agent -o wide
$ kubectl delete ds fluentd-agent
$ kubectl get ds,po -l k8s-app=fluentd-agent
```
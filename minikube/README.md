# MINIKUBE: Instalando Cluster Kubernetes local

Após estudos de conceitos introdutórios sobre Kubernetes, arquictetura, ferramentas de instalação e outros; estou avançando para parte práctica. Vou começar por instalar o Minikube na minha máquina Linux. Para instalares na tua máquina também, siga a [documentação do minikube](https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download).

Feito isso, bora para o mundo do Kubernetes!!!

## Comandos Essenciais

```bash
$ minikube start
$ minikube stop
$ minikube delete
```

## Avançando nos recursos do Minikube: Parte 1

### Profile

Um **profile** é como uma instância separada de cluster Kubernetes criada pelo Minikube.

Comandos:

```bash
$ minikube profile list
$ minikube profile <nome_do_profile>
```

## Avançando nos recursos do Minikube: Parte 2

### Nodes

Comandos:

```bash
$ minikube node list
```

## Kubectl

Instalei separadamente o [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/).

### Comandos

```bash
$ kubectl config view
$ kubectl cluster-info
```

## Kubernetes Dashboard

```bash
$ minikube addons list
$ minikube addons enable metrics-server
$ minikube addons enable dashboard
$ minikube dashboard
```
## APIs com kubectl proxy

```bash
$ kubectl proxy
```
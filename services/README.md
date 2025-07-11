# Services

[Manifest Deployment](frontend-deploy.yaml)
[Manifest Service](frontend-svc.yaml)

## Comandos prácticos

```bash
$ kubectl create -f frontend-svc.yaml
```

```bash
$ kubectl expose deploy frontend --name=frontend-svc \
--port=80 --target-port=5000
```

```bash
$ kubectl create service clusterip frontend \
--tcp=80:5000 --dry-run=client -o yaml \
| sed 's/name: frontend/name: frontend-svc/g' \
| kubectl apply -f -
```

```bash
# Warning: v1 Endpoints is deprecated in v1.33+; use discovery.k8s.io/v1 EndpointSlice
$ kubectl get service,endpoints frontend-svc
$ kubectl get svc,ep frontend-svc
```

## Kube-Proxy

[Kube-Proxy Documentation](https://kubernetes.io/docs/concepts/services-networking/service/#virtual-ips-and-service-proxies)

## Traffic Policies

[Traffic Policies Documentation](https://kubernetes.io/docs/reference/networking/virtual-ips/#traffic-policies)

Existem duas opções:

1. Cluster (O padrão)

A opção de cluster permite que o Kube-Proxy segmente alvo todos os pontos de extremidade prontos do serviço no processo de balanceamento de carga. Esse é o comportamento padrão do serviço, mesmo quando a propriedade da política de tráfego não é declarada explicitamente.

2. Local

A opção local , no entanto, isola o processo de balanceamento de carga para incluir apenas os pontos de extremidade do serviço localizado no mesmo nó que o Pedrester POD, ou talvez o nó que capturou o tráfego externo de entrada em seu Nodeport (o tipo de serviço NodEport será abordado em uma aula futura). Embora isso pareça uma opção ideal, ele possui uma falha - se o serviço não tiver um ponto de extremidade pronto no nó em que o POD do solicitante estiver em execução, o serviço não direcionará a solicitação aos pontos de extremidade em outros nós para satisfazer a solicitação porque será descartada pelo Kube -Proxy.

## Service Discovery

Métodos para descoberta de serviços:

1. Variáveis de Ambiente
2. DNS

Comando:

```bash
$ kubectl exec client-app-pod-name -c client-container-name -- /bin/sh -c curl -s frontend-svc:80
```

## ServiceType

[ServiceType Documentation](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types)

### 1. ClusterIP

[ClusterIP Manifest](./servicetype/frontend-clusterip-svc.yaml)

### 2. NodePort

[NodePort Manifest](./servicetype/frontend-nodeport-svc.yaml)

Comandos:

```bash
$ kubectl expose deploy frontend --name=frontend-svc \
--port=80 --target-port=5000 --type=NodePort 
```

```bash
$ kubectl create service nodeport frontend-svc \
--tcp=80:5000 --node-port=32233 
```

### 3. LoadBalancer

[LoadBalancer](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)

### 4. ExternalIP

[ExternalIP](https://kubernetes.io/docs/concepts/services-networking/service/#external-ips)

### 5. ExternalName

[ExternalName](https://kubernetes.io/docs/concepts/services-networking/service/#externalname)

### 6. Multi-Port Services

[Multi-Port Manifest](./servicetype/frontend-multiport-svc.yaml)

### 7. Port-Forwading

Comandos:

```bash
$ kubectl port-forward deploy/frontend 8080:5000 
```

```bash
$ kubectl port-forward frontend-77cbdf6f79-qsdts 8080:5000 
```

```bash
$ kubectl port-forward svc/frontend-svc 8080:80 
```
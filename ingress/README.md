# Ingress

Ingress configura um balanceador de carga HTTP/HTTPS da camada 7 para serviços e fornece o seguinte:

- TLS (Transport Layer Security)
- [Name-based virtual hosting](https://kubernetes.io/docs/concepts/services-networking/ingress/#name-based-virtual-hosting)
- [Fanout routing](https://kubernetes.io/docs/concepts/services-networking/ingress/#simple-fanout)
- Loadbalancing
- Custom rules.

## Name-based virtual hosting

[Manifest Ingress 1](named-based-virtual-hosting.yaml)

## Fanout routing

[Manifest Ingress 2](fanout.yaml)

## Ingress Controller

[Ingress Controller](https://www.nginx.com/products/nginx/kubernetes-ingress-controller)

```bash
$ minikube addons enable ingress 
```

```bash
$ kubectl create -f named-based-virtual-hosting.yaml
```

## Access Services Using Ingress

```bash
$ sudo vim /etc/hosts
```
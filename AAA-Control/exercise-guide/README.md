# Exercício Guiado

```bash
$ minikube start
$ kubectl config view
```

```bash
$ kubectl create namespace lfs158
$ mkdir rbac
$ cd rbac/
```

```bash
~/rbac$ sudo useradd -s /bin/bash bob
~/rbac$ sudo passwd bob
# senha: teste123
```

```bash
~/rbac$ openssl genrsa -out bob.key 2048
```

```bash
~/rbac$ openssl req -new -key bob.key \
  -out bob.csr -subj "/CN=bob/O=learner"
```

```bash
~/rbac$ vim signing-request.yaml
```

```bash
~/rbac$ cat bob.csr | base64 | tr -d '\n','%'
```

```bash
~/rbac$ kubectl create -f signing-request.yaml
```

```bash
$ kubectl get csr
```

```bash
~/rbac$ kubectl certificate approve bob-csr
```

```bash
$ kubectl get csr
```

```bash
~/rbac$ kubectl get csr bob-csr \
  -o jsonpath='{.status.certificate}' | \
  base64 -d > bob.crt
```

```bash
~/rbac$ cat bob.crt
```

```bash
~/rbac$ kubectl config set-credentials bob \
  --client-certificate=bob.crt --client-key=bob.key
```

```bash
~/rbac$ kubectl config set-context bob-context \
  --cluster=minikube --namespace=lfs158 --user=bob
```

```bash
~/rbac$ kubectl config view
```

```bash
~/rbac$ kubectl -n lfs158 create deployment nginx --image=nginx:alpine
```

```bash
~/rbac$ kubectl --context=bob-context get pods
```

```bash
~/rbac$ vim role.yaml
```

```bash
~/rbac$ kubectl create -f role.yaml
```

```bash
~/rbac$ kubectl -n lfs158 get roles
```

```bash
~/rbac$ vim rolebinding.yaml
```

```bash
~/rbac$ kubectl create -f rolebinding.yaml
```

```bash
~/rbac$ kubectl -n lfs158 get rolebindings
```

```bash
~/rbac$ kubectl --context=bob-context get pods
```
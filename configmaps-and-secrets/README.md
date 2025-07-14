# ConfigMaps and Secrets

## ConfigMaps

### Criar um ConfigMap de Literal Values

```bash
$ kubectl create configmap my-config \
  --from-literal=key1=value1 \
  --from-literal=key2=value2
```

```bash
$ kubectl get configmaps my-config -o yaml
```

### Criar um ConfigMap da Definição de um Manifest

[Manifest ConfigMap](customer1-configmap.yaml)

```bash
$ kubectl create -f customer1-configmap.yaml
```

### Criar um ConfigMap de um ficheiro

[Ficheiro de exemplo](permission-reset.properties)

```bash
$ kubectl create configmap permission-config \
  --from-file=permission-reset.properties
```

### ConfigMaps inside Pods: Variáveis de Ambiente

Situação de uso: Muitos valores que podem ser usados diretamente como variáveis de ambiente.

[Exemplo](./configmaps-inside-pods/myapp-full-container)

Situação de uso: Precisa apenas de 1 ou 2 chaves específicas.

[Exemplo](./configmaps-inside-pods/myapp-specific-container)

### ConfigMaps inside Pods: Volumes

[Exemplo](./configmaps-inside-pods/vol-config-map)

[Exercício Guiado](./exercise-guide-configmaps/)

***

## Secrets

### Criar um Secret de Literal Values

```bash
$ kubectl create secret generic my-password \
  --from-literal=password=mysqlpassword
```

```bash
$ kubectl get secret my-password
```

```bash
$ kubectl describe secret my-password
```

### Criar um Secret da Definição de um Manifest

```bash
$ echo mysqlpassword | base64
```

[Manifest com Type data](mypass-data.yaml)

[Manifest com Type stringData](mypass-stringdata.yaml)

```bash
$ kubectl create -f mypass-stringdata.yaml
```

### Criar um Secret de um ficheiro

```bash
$ echo mysqlpassword | base64
```

```bash
$ echo -n 'bXlzcWxwYXNzd29yZAo=' > password.txt
```

```bash
$ kubectl create secret generic my-file-password \
  --from-file=password.txt
```

```bash
$ kubectl get secret my-file-password
```

```bash
$ kubectl describe secret my-file-password
```

### Secrets inside Pods: Variáveis de Ambiente

[Manifest](./secrets-inside-pods/mypass-spec-container.yaml)

### ConfigMaps inside Pods: Volumes

[Manifest](./secrets-inside-pods/vol-secret.yaml)
# Advanced Topics

## Annotations

[Annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/)

Formato key-value:

```yaml
"annotations": {
  "key1": "value1",
  "key2": "value2"
}
```

### Anotar um pod existente

```bash
$ kubectl annotate pod mypod key1=value1 key2=value2
```

### Anotar numa Definição de Manifest

[Manifest](annotate.yaml)

### Gravar configurações atuais no Annotations

```bash
$ kubectl run saved --image=nginx:alpine --save-config=true
```

```bash
$ kubectl get pod saved -o yaml
```

## Quota and Limits Management


### Quota

Tipos de quota por namespace:

1. **Compute Resource Quota**

We can limit the total sum of compute resources (CPU, memory, etc.) that can be requested in a given Namespace.

[Manifest Example](./quota-and-limits-management/compute-quota.yaml)

2. **Storage Resource Quota**

We can limit the total sum of storage resources (PersistentVolumeClaims, requests.storage, etc.) that can be requested.

3. **Object Count Quota**

We can restrict the number of objects of a given type (Pods, ConfigMaps, PersistentVolumeClaims, ReplicationControllers, Services, Secrets, etc.).

[Manifest Example](./quota-and-limits-management/object-quota.yaml)

### Limits Management

An additional resource that helps limit resource allocation to pods and containers in a namespace, is the LimitRange, used in conjunction with the ResourceQuota API resource. A LimitRange can:

- Set compute resources usage limits per Pod or Container in a namespace.
- Set storage request limits per PersistentVolumeClaim in a namespace.
- Set a request to limit ratio for a resource in a namespace.
- Set default requests and limits and automatically inject them into Containers' environments at runtime.

[Manifest Example](./quota-and-limits-management/limit-mngmt.yaml)

## Autoscaling

1. [Horizontal Pod Autoscaler](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)

This HPA dynamically triggers the scaling of a myapp Deployment when CPU reaches 80% utilization, between 2 and 10 replicas: 

```bash
kubectl autoscale deploy myapp --min=2 --max=10 --cpu-percent=80
```

2. [Vertical Pod Autoscaler](https://github.com/kubernetes/autoscaler/tree/master/vertical-pod-autoscaler#readme)

3. [Cluster Autoscaler](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler#cluster-autoscaler)

## Jobs and CronJobs

### [Jobs](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/) no Kubernetes

Um Job é usado quando você quer executar uma tarefa uma única vez, e garantir que ela será concluída com sucesso, mesmo que o Pod falhe no meio do caminho.

Exemplo de uso:

- Processar um arquivo.
- Enviar e-mails em lote.
- Aplicar uma migração de banco.

Comportamento:

- Ele cria um ou mais Pods para executar a tarefa.
- Se um Pod falhar, o Job cria outro automaticamente.
- Assim que a tarefa termina, os Pods são removidos (ou aguardam o tempo de limpeza definido com `ttlSecondsAfterFinished`).

Parâmetros importantes de um Job:

Parâmetro | O que faz
:---: | :---:
parallelism | Quantos Pods podem rodar ao mesmo tempo.
completions | Quantas vezes a tarefa precisa ser completada.
backoffLimit | Quantas vezes pode falhar antes de ser marcado como "falhou".
activeDeadlineSeconds | Tempo máximo para o Job terminar, senão será interrompido.
ttlSecondsAfterFinished | Tempo para o Kubernetes limpar o Job após terminar.

[Exemplo básico de Job](./jobs-and-cronjobs/job-example.yaml)

### [CronJobs](https://kubernetes.io/docs/tasks/job/automated-tasks-with-cron-jobs/) no Kubernetes

Um CronJob é como um Job, mas com agendamento, ou seja, você define quando o Job deve ser executado, periodicamente.

Exemplo de uso:

- Fazer backup todo dia às 02h.
- Limpar dados temporários a cada 10 minutos.
- Enviar relatórios semanais.

Funcionamento:

- A cada intervalo definido (formato cron), um novo Job é criado.
- Cada Job tem os mesmos parâmetros que vimos anteriormente.
- Ideal para tarefas recorrentes.

Parâmetros importantes do CronJob:

Parâmetro | O que faz
:---: | :---:
schedule | Cron expression (ex: "0 2 * * *" para 2h da manhã)
startingDeadlineSeconds | Tolerância de atraso (se estiver atrasado, ignora ou executa?)
concurrencyPolicy | Pode rodar vários ao mesmo tempo? (Allow, Forbid, Replace)
successfulJobsHistoryLimit/failedJobsHistoryLimit | Quantidade de históricos mantidos.

[Exemplo de CronJob]()


### Comparação Final

Recurso | Execução | Agendamento? | Repetição? | Uso típico
:---: | :---: | :---: | :---: | :---:
Job | Uma vez | ❌ | ❌ | Script de migração, tarefa pontual
CronJob | Recorrente | ✅ | ✅ | Backups, relatórios, manutenção

## StatefulSets

[StatefulSets](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)

## Recursos Personalizados

Existem duas maneiras de adicionar recursos personalizados:

- [Definições de recursos personalizados (CRDS)](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)

- [Agregação da API](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/apiserver-aggregation/)

## [Security Contexts](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/) and Pod Security Admission

[Manifest](./security-contexts/security-contexts.yaml)

## [Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

[Manifest](./network-policies/network-policy.yaml)

## Monitoring, Logging, and Troubleshooting

$ kubectl logs pod-name

$ kubectl logs pod-name container-name

$ kubectl logs pod-name container-name -p

$ kubectl exec pod-name -- ls -la /

$ kubectl exec pod-name -c container-name -- env

$ kubectl exec pod-name -c container-name -it -- /bin/sh

$ kubectl get events

$ kubectl events

$ kubectl describe pod pod-name


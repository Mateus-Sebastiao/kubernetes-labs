# Kubernetes Volume Management

## Tipos de Volume

[Documentation](https://kubernetes.io/docs/concepts/storage/volumes/#volume-types)

Alguns exemplos de tipos de volume que suportam volumes efêmeros são:

- emptyDir
- hostPath
- [gcePersistentDisk](https://cloud.google.com/compute/docs/disks/)
- [awsElasticBlockStore](https://aws.amazon.com/ebs/)
- [azureDisk](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/managed-disks-overview)
- [azureFile](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_file)
- [cephfs](https://ceph.io/ceph-storage/)
- [nfs](https://github.com/kubernetes/examples/tree/master/staging/volumes/nfs)
- [iscsi](https://github.com/kubernetes/examples/tree/master/volumes/iscsi)
- [secret](https://kubernetes.io/docs/concepts/configuration/secret/)
- [configMap](https://kubernetes.io/docs/concepts/configuration/configmap/)
- [persistentVolume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

- [persistentVolumeClaim](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)

Há quatro modos de acesso: ReadWriteOnce (leitura e gravação por um único nó), ReadOnlyMany (somente leitura por vários nós), ReadWriteMany (leitura e gravação por vários nós) e ReadWriteOncePod (leitura e gravação por um único pod).
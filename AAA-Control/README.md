# Controle de Autenticação, Autorização e Admissão

## Autenticação

[Authentication](https://kubernetes.io/docs/reference/access-authn-authz/authentication/)

O kubernetes suporta dois tipos de [usuarios](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#users-in-kubernetes):

1. Normal Users;
2. Service Accounts

Para autenticação, usa os seguintes [modulos de autenticação](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#authentication-strategies):

- X509 Client Certificates
> --client-ca-file=SOMEFILE
- Static Token File
- Bootstrap Tokens
- Service Account Tokens
- OpenID Connect Tokens
- Webhook Token Authentication
- Authenticating Proxy

## Autorização

[Authorization](https://kubernetes.io/docs/reference/access-authn-authz/authorization/)

### Modos de autorização

#### Nodes

[Node Authorization Documentation](https://kubernetes.io/docs/reference/access-authn-authz/node/)

#### Attribute-Based Access Control (ABAC)

[Attribute-Based Access Control (ABAC)](https://kubernetes.io/docs/reference/access-authn-authz/abac/)

Ficheiro de [exemplo](./authorization/ABAC/PolicyFile.json)

Para ativar o modo ABAC, iniciamos o servidor de API com a opção -authorization-mode=ABAC, enquanto especificamos a política de autorização com -authorization-policy-file=PolicyFile.json.

#### Webhook

[Webhook mode documentation](https://kubernetes.io/docs/reference/access-authn-authz/webhook/)

Para ativar o autorizador do Webhook, precisamos iniciar o servidor de API com a opção -authorization-webhook-config-file=SOME_FILENAME, onde SOME_FILENAME é a configuração do serviço de autorização remota.

#### Role-Based Access Control (RBAC)

[RBAC Mode](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

O modo RBAC pode criar dois tipos de `Roles`:

1. Role
2. ClusterRole


Ficheiro de exemplo do tipo [Role](./authorization/RBAC/type_role.yaml)
Ficheiro de exemplo do tipo [ClusterRole](./authorization/RBAC/type_rolebinding.yaml)

Assim que o `Role` está criado, podemos ligar para usuários com o `RoleBinding` object. Existem dois tipos de RoleBindings:

1. RoleBinding
2. ClusterRoleBinding

Ficheiro de exemplo do tipo [RoleBinding](./authorization/RBAC/type_rolebinding.yaml)

Ficheiro de exemplo do tipo [ClusterRoleBinding](./authorization/RBAC/type_clusterrolebinding.yaml)
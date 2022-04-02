# EPAM24 K8s

## task04_user_deploy_view.yaml
Creates ClusterRoleBinding and ClusterRole which give to the user deploy_view
rights only to view deployments and pods in a cluster.

## task04_user_deploy_edit.yaml
Creates ClusterRoleBinding and ClusterRole which give to the user deploy_edit
full rights to the objects deployments and pods in a cluster.

## task04_user_prod_view.yaml
Creates RoleBinding which reference a ClusterRole "view" to grant view rights
on namespace prod.

## task04_user_prod_admin.yaml
Creates RoleBinding which reference a ClusterRole "admin" to grant admin rights
on namespace prod.

## task04_sa_namespace_admin.yaml
The manifest creates a ServiceAccount "sa-namespace-admin" and grants full rights
to a namespace "default".


## Configure user authentication

### Create certificate for new user:
```bash
openssl genrsa -out new_user_name.key 2048
openssl req -new -key new_user_name.key -out new_user_name.csr -subj "/CN=new_user_name"
```
!!!if you are facing a name format problem, try "//CN=new_user_name"!!!
```bash
openssl x509 -req -in new_user_name.csr -CA ~/.minikube/ca.crt \
-CAkey ~/.minikube/ca.key -CAcreateserial -out new_user_name.crt -days 500
```
### Edit ~/.kube/config

### Add user:
```bash
users:
- name: new_user_name
  user:
    client-certificate: ..\new_user_name.crt (change path)
    client-key: ..\new_user_name.key (change path)
```
If you are using token authentication:
```bash
users:
- name: new_user_name
  user:
    token: token-base64-decoded
```

### Add context:
```bash
contexts:
- context:
    cluster: cluster_name (for example: minikube)
    user: new_user_name
  name: new_user_name
```

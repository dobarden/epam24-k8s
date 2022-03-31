# EPAM24 K8s
## task03-deploy.yaml and task03-ingress.yaml
The manifests publish minio "outside" using ingress. By minikube_ip returning minio, by path minikube_ip/web returning nginx.
## task03-deploy-emptydir.yaml
Creates deployment with emptyDir.
## task03-nfs-pv.yaml, task03-nfs-pvc.yaml and task03-deploy-nfs.yaml
The manifests create a pv using nfs share, create a pvc for it, create a deployment.

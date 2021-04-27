# Minikube
- `minikube version`
- `minikube start`

# Kubectl
- `kubectl version`
- `kubectl cluster-info` cluster details
- `kubectl get nodes` view nodes in cluster

## Kubectl deployment
- `kubectl get deployments`
- `kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1` create a deployment (define a name and the image to be used)

## Kubectl proxy
- `kubectl proxy` opens a direct connection to cluster so we can access the pods

## Kubectl pod
- `kubectl logs POD_NAME`
- `kubectl exec POD_NAME -- ls`(here calling **ls** from the pod but can be any command)
- `kubectl exec -it POD_NAME -- bash`

## Kubectl Services
- Services can be exposed in different ways
    - **ClusterIp (default)**: Exposes the Service on a internal IP in the cluster. Service only within the cluster (therefore `kubectl proxy`)
    - **NodePort**: Exposes each service on the same port of each separate node (the service can be accessed from outside the cluster using `Node_IP`:`Node_Port`)
    - **LoadBalancer**: Creates an external load balancer in the current cluster and assigns a fixed external ip to the service.
    - **ExternalName**: Maps the service to the contents of the `externalName`field (`xyz.com`). This type requires v1.7+ of kube-dns, or CoreDNS version 0.0.8+.
- `kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080` exposes a deployment as a NodePort service under the port 8080
- `kubectl delete service --selector app=kubernetes-bootcamp` delete by label
- `kubectl delete service/servicename` delete by service name

## Kubectl Labels
- List pod/deployment/replicasSet/service labels: `kubectl get pods --show-labels`
- Add labels to running pods: `kubectl label pod/helloworld app=mhgf`
- Delete label: `kubectl label pod/helloworld app-` (deleting app label)
- Filter by label: `kubectl get posts [--selector|-l] env=production` (filter all pods which label is env=production)
- Filter by multiple labels: `kubectl get posts [--selector|-l] env=production,devlead=carisa` (filter all pods which label is env=production)

## Kubectl App Scale
- Scale up/down a deployment: `kubectl scale deployments/kubernetes-bootcamp --replicas=4`

## Kubectl Update Deployment
- `kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v2` (provide image for deployment)
- Scale up/down a deployment: `kubectl scale deployments/kubernetes-bootcamp --replicas=4`
- Confirm an update: `kubectl rollout status deployments/kubernetes-bootcamp`
- Rollback an update: `kubectl rollout undo deployments/kubernetes-bootcamp`

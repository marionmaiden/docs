# Minikube
- `minikube version`
- `minikube start`

# Kubectl
- `kubectl version`
- View cluster details: `kubectl cluster-info`
- View nodes within a cluster: `kubectl get nodes`
- Get contexts: `kubectl config get-contexts`
- Get context in use: `kubectl config current-context`

## Kubectl deployment
- Get deployments in cluster: `kubectl get deployments`
- Create a deployment (define a name and the image to be used): `kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1`
- Create a deployment from file: `kubectl create -f file.yaml`
- Create or update a deployment: `kubectl apply -f file.yaml`

## Kubectl proxy
- `kubectl proxy` opens a direct connection to cluster so we can access the pods

## Kubectl pod
- Visualizes the pod logs: `kubectl logs POD_NAME`
- Run command over a pod: `kubectl exec POD_NAME -- ls`(here calling **ls** from the pod but can be any command)
- Open bash over a pod: `kubectl exec -it POD_NAME -- bash`

## Kubectl Services
- Services can be exposed in different ways
    - **ClusterIp (default)**: Exposes the Service on a internal IP in the cluster. Service only within the cluster (therefore `kubectl proxy`)
    - **NodePort**: Exposes each service on the same port of each separate node (the service can be accessed from outside the cluster using `Node_IP`:`Node_Port`)
    - **LoadBalancer**: Creates an external load balancer in the current cluster and assigns a fixed external ip to the service.
    - **ExternalName**: Maps the service to the contents of the `externalName`field (`xyz.com`). This type requires v1.7+ of kube-dns, or CoreDNS version 0.0.8+.
- Exposes a deployment as a NodePort service under the port 8080: `kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080`
- Delete service by label: `kubectl delete service --selector app=kubernetes-bootcamp`
- Delete by service name: `kubectl delete service/servicename`

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

## Kubectl Secrets
- List secrets: `kubectl get secrets`
- List decoded secrets (requires **jq**): `kubectl get secret secret_name -o json | jq '.data | map_values(@base64d)'` 
- View secret file: `kubectl get secret secret_name -o yaml`
- Create a secret: `kubectl create secret generic secret_name`
- Describe the entries in a secret: `kubectl describe secret secret_name`
- Edit a secrets file: `kubectl edit secret dispatcher`
- Apply a secret file: `kubectl apply -f stage_sec.yaml`

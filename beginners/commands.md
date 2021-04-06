##### Show all created kubernetes elements
`kubectl get all`
##### Show yaml definition of the kubernetes element
`kubectl get ${element} -o yaml`
##### Show detailed information about the kubernetes element
`kubectl describe ${element} elementName`
##### Create kubernetes element with cli from file
- `kubectl create -f element-definition.yml`
- `kubectl apply -f element-definition.yml`
##### Update kubernetes element with cli from file
- `kubectl replace -f element-definition.yml`
- `kubectl apply -f element-definition.yml`
##### Edit kubernetes element with cli with in-memory temp file
Changes are not persisted!

`kubectl edit ${element} elementName`
##### Delete kubernetes element with cli
`kubectl delete ${element} elementName`

#### Note:
`element=[pod, replicaset, deployment, service]`

#### Pod:
##### Show the running pods: name, ready, status, restarts, age
`kubectl get pods`
##### Show the running pods with extra info: ip, node, nominated node, readiness gates
`kubectl get pods -o wide`
##### Create pod with cli
`kubectl run nginx --image=nginx`
##### Create pod definition file
`kubectl run podName --image=dockerContainerName --dry-run=client -o yaml > pod-definition.yml`
##### options for run/create
- `--name=nginx-pod`
- `--image=nginx:alpine`
- `--labels=tier=db`


#### Replicaset:
##### Show the running replica-sets: name, desired, current, age
`kubectl get replicaset`
##### scale
- `kubectl scale --replicas=6 -f replicaset-definition.yml`
- `kubectl scale replicaset myapp-replicaset --replicas=6`

#### Deployment:
##### Show the running deployments: name, up-to-date, available, age
`kubectl get deployments`
##### Create deployment with cli
`kubectl create deployment deploymentName --image=dockerContainer --replicas=3`
##### Create deployment with record (it can be seen in the rollout history)
`kubectl create -f deployment-definition.yml --record`
##### Show status of the deployment
`kubctl rollout status deployment/myapp-deployment`
##### Show rollout history of the deployment
`kubctl rollout history deployment/myapp-deployment`
##### Rollback deployment
`kubectl rollout undo deployment/myapp-deployment`

#### Service:
##### Show the running services: name, type, cluster-ip, port(s), age
`kubectl get services`
##### Get url with minikube
`minikube service myapp-service --url`
##### options for run/create
- `--port 6379`
- `--target-port 6379`

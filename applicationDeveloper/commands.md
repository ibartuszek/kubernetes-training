##### Cluester info
`kubectl cluster-info

#### Namespaces
##### Get all namespaces
`kubectl get ns`

##### Create namespace
`kubectl create namespace dev`

##### Change the namespace
`kubectl config set-context $(kubectl config current-context) --namespace=dev`

##### Add namespace to commands
- without definition kubernetes creates everything in default namespace

`kubectl create -f pod-definition.yml --namespace=dev`
`kubectl get pods --all-namespaces`

#### Dry run
- to create definition files
- with `-o yaml` option
- deployment:

`kubectl create deployment --image=nginx nginx --dry-run -o yaml > nignx-deployment.yaml`

- service: (clusterIp)

`kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml`

- service: (nodeport)

`kubectl expose pod nginx --port=80 --name nginx-service --type=NodePort --dry-run=client -o yaml`

##### Create pod with service
`kubectl run httpd --image=httpd:alpine --port --expose --dry-run=client -o yaml`

##### Create configmap
###### --from-literal=\<key\>=\<value\>
```
kubectl create configmap \
  app-config --from-literal=APP_COLOR=blue \
             --from-literal=APP_MOD=prod
```
###### --from-file=\<path-to-file\>
```
kubectl create configmap <config-name> --from-file=app_config.properties
```
##### Create secret
```
kubectl create secret \
  app-secret --from-literal=DB_HOST=mysql \
             --from-literal=APP_USER=root
```
###### --from-file=\<path-to-file\>
```
kubectl create secret <secret-name> --from-file=app_secret.properties
```

##### Service accounts
###### Create
`kubectl create serviceaccount dashboard-sa`

##### Taints
- on nodes
`kubectl taint nodes node-name key=value:taint-effect`
- taint effects:
  - NoSchedule
  - PreferNoSchedule
  - NoExecute -> no new pods
`kubectl taint nodes node1 app=blue:NoSchedule`

- to remove:
`kubectl taint nodes node-name key=value:taint-effect-`

##### Label nodes
- limited -> use node affinity instead
`kubectl label nodes <node-name> <label-key>=<label-value>`

###### example call
`curl https://192.168.56.70:6443/api -insecure -- header "Authorization: Bearer ..."`

##### Other commands
###### Get help
`kubectl explain pods --recursive | less`

###### Copy part (8 lines from enfFrom word)
`kubectl explain pods --recursive | grep -A8 envFrom`

###### Run custom command on pod
`kubectl exec -it ubuntu-sleeper -- date -s '19 APR 2012 11:14:00'`
`kubectl exec webapp -- cat /log/app.log`
`kubectl -n elastic-stack exec -it app cat /log/app.log`

###### Check logs
`kubectl logs app`
####### live logs
`kubectl logs -f app`
####### logs with multiple containers
`kubectl logs app container`

##### metrics
###### enable minikube
`minikube addons enable metrics-server`

###### get node consumption
`kubectl top node

###### Ingress`
###### Create ingress definition file
`kubectl -n ingress-space expose deployment ingress-controller --name ingress --port 80 --target-port 80 type NodePort --dry-run=client -o yaml > ingress-svc.yml `
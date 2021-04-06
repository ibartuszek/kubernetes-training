##### Cluester info
`kubectl cluster-info

#### Namespaces
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
### k8's headless service 

![[Screenshot 2026-11-06 at 3.05.12 PM.png]]
DNS - given a domain name it resolves into ip address
A record - resolves domain to address
CName-alias
nslookup![[Screenshot 2026-11-06 at 3.18.33 PM.png]]How do we create domain names in Kubernetes
Service gives you domain names on your pods

kubectl get pods
kubectl services --help
kubectl | grep help

kubectl exec -it stooge-0 --sh
kubectl get pods

`#hostname`
`# curl http://stooge-1:8080/hello`

pod - virutal machine
multiple pods can be run on a machine
pods can run multiple containers

headless service
statefulset

scale talk - too late

kubectl rollout restart statefulset

go func() {
  // tick every 5 sec
  // iterate over peers
}

kind create cluster

ticker := time.NewTicker(5 * time.Second)

docker build -t ...
/load the image
kubectl load logs

etcd-raft


HW:

DNS Tables - IP Tables
Video on IP Tables DNS 

Service is an abstration
namespace - collection of named for resources
gamma
betta

ip trables are running on nodes
nodes are the physical machines
pods run on nodes 
worker nodes


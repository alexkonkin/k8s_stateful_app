# k8s_stateful_app
to deploy:
- create volume claims and volumes
  kubectl apply -f volume_claim_init_sql.yml,volume_claim_mysql_data.yml

- create database deployment and service
  kubectl apply -f mysql_578.yml

- create petclinic deployment and service
kubectl apply -f petclinic.yml

- create service that exposes application via the cluster ip
  kubectl expose deployment petclinic --name=clusterip --port=80 --target-port=8080 

- configure nginx to proxy traffic to this ip

to delete:
kubectl delete deployment,svc db petclinic
kubectl delete pvc mysql-data-claim mysql-init-claim
kubectl delete pv mysql-data-volume mysql-init-volume

get an IP of the petclinic service:
kubectl describe service petclinic

run diagnostic container:
kubectl run -i --tty --rm debug --image=busybox --restart=Never -- sh

get pods on all nodes:
kubectl get pod -o=custom-columns=NAME:.metadata.name,STATUS:.status.phase,NODE:.spec.nodeName --all-namespaces

-----
expose:
1. kubectl expose deployment petclinic --name=clusterip --port=80 --target-port=8080
and then add nginx to proxy from real ip to the ip of the 
pet
service

2. kubectl expose deployment petclinic --name=nodeport --port=80 --target-port=8080 --type=NodePort

3. kubectl expose deployment petclinic --name=loadbalancer --port=80 --target-port=8080 --type=LoadBalancer

other useful info:
k8s cheat sheet:
https://kubernetes.io/docs/reference/kubectl/cheatsheet/
exposing app to the external world
https://kubernetes.io/docs/tutorials/services/source-ip/


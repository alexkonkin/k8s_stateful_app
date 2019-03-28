# k8s_stateful_app

to deploy:
- create volume claims and volumes
kubectl apply -f volume_claim_init_sql.yml,volume_claim_mysql_data.yml
- create database deployment and service
kubectl apply -f mysql_578.yml

- create petclinic deployment and service
kubectl apply -f petclinic.yml

to delete:
kubectl delete deployment,svc db petclinic
kubectl delete pvc mysql-data-claim mysql-init-claim
kubectl delete pv mysql-data-volume mysql-init-volume

get an IP of the petclinic service:
kubectl describe service petclinic

run diagnostic container:
kubectl run -i --tty --rm debug --image=busybox --restart=Never -- sh

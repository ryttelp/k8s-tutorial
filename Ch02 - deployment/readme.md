# Init
```Shell
# Utworzenie namespace
k create ns k8s-tutorial
# Zmiana namespace   
kubectl config set-context --current --namespace=k8s-tutorial

kubectl create secret docker-registry regcred --docker-server=https://index.docker.io/v1/ --docker-username=ryttelp --docker-password=xxxxxxx --docker-email=pawel.ryttel@gmail.com
```
# Jeden pod
```
# Tworzymy poda z cli
k run hello --image hello-kubernetes:1.1

k get pods --watch

k describe pod hello
# błąd pobrania

k delete pod hello

# tworzymy pullsecret
kubectl create secret docker-registry regcred --docker-server=https://index.docker.io/v1/ --docker-username=ryttelp --docker-password=xxxxxxx --docker-email=pawel.ryttel@gmail.com
# albo tak
k apply -f secret.yaml 
# tworzymy jeszcze raz poda
k apply -f pod.yaml 

# podgląd poda
k port-forward hello 30444:8080
curl http://localhost:30444

#pod na porcie node'a
k expose pod hello --type NodePort  


```
# Prosty deployment
# Statefulset (PVki)
# Rolling deployments

# Init
```Shell
# Utworzenie namespace
k create ns k8s-tutorial
# Zmiana namespace   
kubectl config set-context --current --namespace=k8s-tutorial

kubectl create secret docker-registry regcred --docker-server=docker.io --docker-username=ryttelp  --docker-email=pawel.ryttel@gmail.com --docker-password=xxxxxxx
oc secrets link default regcred --for=pull
```
Polecenia oc
https://docs.openshift.com/container-platform/4.7/cli_reference/openshift_cli/developer-cli-commands.html

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
oc secrets link default regcred --for=pull
# albo tak
k apply -f secret.yaml 
# tworzymy jeszcze raz poda
k apply -f pod.yaml 

# podgląd poda
k port-forward hello 30444:8080
curl http://localhost:30444

#pod na porcie node'a
k expose pod hello --type NodePort  

#l2
oc run --help
oc run -it busybox --rm --image=nexus01.centrala.kaczmarski.pl:8082/docker.io/busybox --restart=Never
```
# Prosty deployment
```
# wdrozenie 
k apply -f deployment.yaml
# skalowanie
k scale deployment --replicas=2 hello
# utworzenie serwisu
k expose deployment hello --name hellod
# utworzenie serwisu NodePort
k expose deployment hello --name hellod --type NodePort
# test
curl http://node-1:32722 | grep "<td>hello-"

# replace
oc replace -f pod.yaml --force
```
# Statefulset (PVki)
``` https://livebook.manning.com/book/kubernetes-in-action-second-edition/chapter-7/v-6/13 - montowanie wolumenów
``` Shareowanie emptydir - https://livebook.manning.com/book/kubernetes-in-action-second-edition/chapter-7/v-6/124

# wdrożenie statefull set
k get pv
k apply -f statefulset-1.yaml
# nie działa - why?
k describe statefulset nginx
k get pv
k get pvc
# ?
k logs www-nginx-0
# uooo
# no to może dodać volume do cache
k apply -f statefulset-2.yaml
# eee. no nie
k logs www-nginx-0
# dodajemy securityContext
k apply -f statefulset-3.yaml
# f...k
# trzeba wyłączyć zabezpieczenie OSH
oc create sa runasanyuid 
oc adm policy add-scc-to-user anyuid -z default

```
# Labels
```
oc run hello2 --image=paulbouwer/hello-kubernetes:1.10 --dry-run=client -o yaml | vi -
oc get pods -l app=hello
```
# Resource Quota

# PodAffinity

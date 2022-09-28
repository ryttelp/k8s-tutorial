
# Instalacja narzędzi

1. instalacja ubuntu z ms store - lts20
2. instalacja cube ctl - https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
3. krew - https://krew.sigs.k8s.io/docs/user-guide/setup/install/
   export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
4. kubectx - https://github.com/ahmetb/kubectx
   kubectl krew install ctx 
   kubectl krew install ns
5.
6. instlacja autocomplete - oh my zsh
   sudo apt install zsh 
   sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
7. code ~/.zshrc
   wkleic 
   plugins=(
      git
      docker
      kubectl
      kubectx
      helm
      oc
    )
   source <(kubectl completion zsh)
   complete -F __start_kubectl k
   alias kctx="kubectx"
   alias kns="kubens"
   alias k="kubectl"
   export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
8. Helm - https://helm.sh/docs/intro/install/
   $ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
   $ chmod 700 get_helm.sh
   $ ./get_helm.sh
8. Lab
 k ns create hw2
 k get nodes -o wide 
 k get pods -o wide --all-namespaces
 k run hello --image gcr.io/hightowerlabs/helloworld
 k describe pod h
 k logs hello1 
 k logs -p hello1   // jak sie restartuje
 k get pod hello1 -o yaml
 k get svc
 k scale --replicas=3 deployment/kubernetes-bootcamp  
 k proxy
 k exec -ti $POD_NAME -- bash
 #Labels
 k get pods -l app=kubernetes-bootcamp
 k label pods $POD_NAME version=v1
 #Update
 k set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v2
 k rollout status deployments/kubernetes-bootcamp
#Edit
export KUBE_EDITOR="code --wait"    
k edit deployment aspmvc-core-sample
#testy
kubectl run -i -t --rm --image=brix4dayz/swiss-army-knife --restart=Never debug  
# Azure k8s
az aks get-credentials --name F1 --resource-group K8s
# Zadanie - Helm
https://github.com/paulbouwer/hello-kubernetes
# Zadanie - kubernetes dashboard
https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
kubectl -n kubernetes-dashboard get secret $(kubectl -n kubernetes-dashboard get sa/admin-user -o jsonpath="{.secrets[0].name}") -o go-template="{{.data.token | base64decode}}"H

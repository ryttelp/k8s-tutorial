# configure nginx with configmap
vi index.html
oc create cm index --from-file=index.html
oc get configmap index -o yaml

vi nginx-pod.yaml
oc create -f nginx-pod.yaml
oc exec -it redis redis-cli

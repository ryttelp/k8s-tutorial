vi deploy.yaml

oc apply -f deploy.yaml

oc get deploy

oc scale deploy/hello-dep --replicas=4

oc expose deploy/hello-dep --port=80 --target-port=8080

curl http://hello-dep.sandbox-p-ryttel

oc get svc

oc delete route hello-dep

oc expose svc/hello-dep



oc get route hello-dep  -o jsonpath='{.spec.host}'

oc annotate route hello-dep haproxy.router.openshift.io/disable_cookies="TRUE" --overwrite=true

oc rollout history deploy/hello-dep

oc patch deploy/hello-dep -p '{"spec":{"strategy":{"rollingUpdate":{"maxUnavailable":"50%","updatePeriodSeconds":"3"}}}}'

oc set image deploy/hello-dep *=nexus01.centrala.kaczmarski.pl:8082/docker.io/paulbouwer/hello-kubernetes:1.10.0 && watch -n 0.5 oc get pods

oc rollout history deploy/hello-dep
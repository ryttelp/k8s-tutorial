# Html to secret
oc create cm index --from-file=index.html
oc apply -f nginx.yaml

# Rolling updates
oc apply -f rolling-deploy.yaml
oc scale deploy hello-roll --replicas=4
oc get po -l app=hello-roll
oc rollout status deploy/hello-roll

oc set image deploy/hello-roll hello-roll=paulbouwer/hello-kubernetes:1
oc rollout history deploy/hello-roll

//oc set image deploy/hello-roll hello-roll=paulbouwer/hello-kubernetes:1 --record=true
//oc annotate deploy/hello-roll kubernetes.io/change-cause="blabla"
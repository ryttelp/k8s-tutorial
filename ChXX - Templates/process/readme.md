vi template.yaml
oc process -f template.yaml --parameters
oc process -f template.yaml -p NAME=test-pod -p TITLE=BleBleBle
oc process -f template.yaml -p NAME=test-pod -p TITLE=BleBleBle | oc create -f -
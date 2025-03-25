# apply helm chart for postgresql

`helm install identitydb oci://registry-1.docker.io/bitnamicharts/postgresql -f postgresql-values.yaml -n opa`

# to install pvc and storage class

`kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/deploy/local-path-storage.yaml`

# note to bound persistent volume claim

`kubectl patch storageclass local-path -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'`

# verify pvc bound and installation

`kubectl get pods -n local-path-storage`

`kubectl get sc`

# keycloak setup

`kubectl apply -f keycloak-cert.yaml`

`kubectl apply -f selfsigned-issuer.yaml`

`kubectl create ns opa`

`helm install keycloak oci://registry-1.docker.io/bitnamicharts/keycloak -f keycloak-values.yaml -n opa`

 

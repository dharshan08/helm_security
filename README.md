# create configmap
`kubectl create configmap bundle-config --from-file=bundle.tar.gz=./config/bundle-server/bundle.tar.gz `
# apply helm chart for opa
`helm repo add opa https://open-policy-agent.github.io/kube-mgmt/charts`

`helm repo update`

`helm upgrade -i -n opa --create-namespace opa opa/opa-kube-mgmt -f opa-values.yaml`

# apply helm chart for postgresql

`helm install identitydb oci://registry-1.docker.io/bitnamicharts/postgresql -f postgresql-values.yaml -n opa`

# to install pvc and storage class

`kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/deploy/local-path-storage.yaml`

# note to bound persistent volume claim

`kubectl patch storageclass local-path -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}`

# verify pvc bound and installation

`kubectl get pods -n local-path-storage`

`kubectl get sc`

# to install pvc and storage class

`kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/deploy/local-path-storage.yaml`

# note to bound persistent volume claim

`kubectl patch storageclass local-path -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'`

# verify pvc bound and installation

`kubectl get pods -n local-path-storage`

`kubectl get sc`

# create namespace

`kubectl create ns opa`

# bundle availability on all ur nodes

`sudo mkdir -p /mnt/data/bundles`

`sudo cp ~/helm_security/bundle.tar.gz /mnt/data/bundles/`

# apply helm chart for bundle-server

`helm upgrade --install bundle-server ./bundle_server -n opa`

# apply helm chart for opa

`helm upgrade --install opa-kafka ./opa -n opa`

# apply helm chart for postgresql

`helm install identitydb oci://registry-1.docker.io/bitnamicharts/postgresql -f postgresql-values.yaml -n opa`

# apply helm chart for keycloak

`helm upgrade --install keycloak ./keycloak -n opa`

 

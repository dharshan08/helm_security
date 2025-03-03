# create configmap
`kubectl create configmap bundle-config --from-file=bundle.tar.gz=./config/bundle-server/bundle.tar.gz `
# apply helm chart for opa
`helm repo add opa https://open-policy-agent.github.io/kube-mgmt/charts`

`helm repo update`

`helm upgrade -i -n opa --create-namespace opa opa/opa-kube-mgmt -f opa-values.yaml`


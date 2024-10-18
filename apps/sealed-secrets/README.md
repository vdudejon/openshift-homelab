# Bitnami Sealed Secrets


## Install kubeseal Client
```bash
sudo dnf install curl jq -y
KUBESEAL_VERSION=$(curl -s https://api.github.com/repos/bitnami-labs/sealed-secrets/tags | jq -r '.[0].name' | cut -c 2-)
curl -OL "https://github.com/bitnami-labs/sealed-secrets/releases/download/v${KUBESEAL_VERSION}/kubeseal-${KUBESEAL_VERSION}-linux-amd64.tar.gz"
tar -xvzf kubeseal-${KUBESEAL_VERSION}-linux-amd64.tar.gz kubeseal
sudo install -m 755 kubeseal /usr/local/bin/kubeseal
```
## Install Sealed Secrets
I was not able to get this to install using OpenShift GitOps, so I installed via helm.
helm repo add sealed-secrets https://bitnami-labs.github.io/sealed-secrets
oc project sealed-secrets
 
helm install sealed-secrets  \
    --set containerSecurityContext.enabled=false \
    --set podSecurityContext.enabled=false \
    sealed-secrets/sealed-secrets  
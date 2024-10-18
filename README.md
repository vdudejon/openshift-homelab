# openshift-homelab
A repo for my OpenShift home lab

## ArgoCD/Red Hat OpenShift GitOps
1. Install Red Hat OpenShift GitOps from the operator hub
2. Edit the Red Hat OpenShift GitOps subscription by adding this to the YAML, which will allow ArgoCD to manage cluster-wide objects
    ```yaml
    apiVersion: operators.coreos.com/v1alpha1
    kind: Subscription
    metadata:
    name: openshift-gitops-operator
    namespace: openshift-gitops-operator
    # ...
    spec:
      config:
        env:
        - name: ARGOCD_CLUSTER_CONFIG_NAMESPACES
          value: openshift-gitops
    # ...
    ```
3. Restart the ArgoCD instance using `oc rollout restart deployment openshift-gitops-server -n openshift-gitops`
